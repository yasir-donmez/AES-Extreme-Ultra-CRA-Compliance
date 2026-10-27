# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## LAB 5 · Zafiyet, Yazılım Envanteri (SBOM) ve Yama Yönetimi
**Raporu Hazırlayan:** AES Group Ar-Ge ve Otomasyon Mühendisliği Ekibi (İmalatçı Perspektifi)  
**Mevzuat ve Standart Hizalaması:** AB Siber Dayanıklılık Yasası (CRA - EU 2024/2847), AB Makine Tüzüğü (2023/1230), IEC 62443-4-1 / IEC 62443-4-2

---

### 📌 1. Giriş ve İmalatçı Yaklaşımı
Bu döküman, AES Group tarafından üretilen **AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı** üzerinde çalışan tüm gömülü yazılımlar, işletim sistemleri, kontrolör derlemeleri ve dikey entegrasyon yazılımlarının **Yazılım Envanterini (SBOM - Software Bill of Materials)** ve bunlara bağlı **Zafiyet / Yama Yönetim Protokolünü** içerir. 

Dışarıdan bir üçüncü taraf gözüyle jenerik "PLC" veya "PC" tanımları yerine; AES Ar-Ge ekibimizin hatta entegre ettiği donanım mimarileri, firma sürümleri, protokol portları ve bilinen güvenlik zafiyetleri (CVE) en ince detayına kadar dokümante edilmiştir.

---

### 📦 2. Bileşen Bazlı Detaylı Yazılım Envanteri (SBOM)

AES Extreme Ultra otomasyon mimarisi 6 ana dijital katmandan oluşmaktadır:

| Bileşen / Alt Sistem | İmalatçı / Tedarikçi | Model / Ürün Kodu | Çalışan Yazılım & Firmware Sürümü | Protokol & Açık Portlar | Kritiklik Seviyesi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **CNC Motion Controller** | Osai Open-Control / AES | Open-4 / AES-CNC Core | RT-Linux Kernel 5.10-rt + Osai WinNCS v4.8.2 | PROFINET RT (Port 34964), EtherCAT, Modbus TCP (Port 502) | **Kritik (Motion & Gantry)** |
| **Safety Controller** | Siemens / SICK | S7-1500F / Flexi Soft | TIA Portal Safety Logic v18.0 / Firmware v2.9.4 | PROFIsafe / PROFINET (UDP Port 34964) | **Kritik (Safety & STO)** |
| **Operatör Arayüzü (IPC / HMI)** | AES Automation | 21.5" Industrial IPC | Windows 10 IoT Enterprise LTSC 2021 + AES TouchHMI v4.2.1 | HTTP (Port 80), HTTPS (Port 443), VNC (Port 5900) | **Yüksek (Operasyon & HMI)** |
| **Uzak Bakım Gateway** | Secomea / Ewon | SiteManager 3329 / Ewon Cosy 131 | SiteManager OS v9.5.6022 / Cosy Firmware v14.4s0 | Outbound TLS/443 (GateManager Proxy), SSH (Port 22) | **Kritik (Dış Erişim Kapısı)** |
| **VFD & Servo Sürücüler** | Yaskawa / Schneider | Sigma-7 Servos / Altivar VFD | Firmware v03.12 (Spindle Driver & Gantry Servos) | EtherCAT / CANopen | **Yüksek (Eksen Torku)** |
| **CAD/CAM & Post-Processor** | Alphacam / NC Hops | Alphacam 2023.1 / NC Hops 7.2 | Post-Processor Engine v3.1 + Barcode Scanner Service | Shared Folder / SMB (Port 445), TCP 8080 | **Orta (Veri Aktarımı)** |

---

### 🔍 3. Gerçek CVE Zafiyet Analizi ve Risk Eşleştirmesi

AES Extreme Ultra üzerinde kullanılan endüstriyel bileşenlerin küresel zafiyet veri tabanlarındaki (NVD / CISA KEV) bilinen zafiyetleri ve makine üzerindeki fiziki etkileri aşağıda analiz edilmiştir:

#### **A. Secomea SiteManager Gateway (Dış Erişim Kapısı)**
* **CVE Kodu:** `CVE-2020-14500` / `CVE-2022-3820`
* **Zafiyet Türü:** Remote Code Execution (RCE) / Buffer Overflow
* **Makinedeki Etkisi:** Saldırgan Secomea gateway'i üzerinden makinenin iç otomasyon ağına (PROFINET) sızabilir, HMI yetkilerini ele geçirebilir ve CNC kodlarına müdahale edebilir.

#### **B. Osai Open-Control CNC Kernel (RTOS)**
* **CVE Kodu:** `CVE-2022-29888` / Unauthenticated VNC & Telnet Access
* **Zafiyet Türü:** Yetkisiz Erişim ve Kimlik Doğrulama Baypası
* **Makinedeki Etkisi:** Port 5900 (VNC) veya Port 23 (Telnet) üzerinden şifresiz bağlantı sağlanarak Spindle 24.000 RPM dönerken Gantry eksen hızları (80 m/dk) aniden değiştirilebilir, takım çarpışmasına (Anti-Crash sensörü baypası) yol açılabilir.

#### **C. Windows 10 IoT HMI & Network Share (SMB)**
* **CVE Kodu:** `CVE-2023-21554` (QueueJumper) / `CVE-2020-0796` (SMBGhost)
* **Zafiyet Türü:** Windows MSMQ ve SMB Remote Code Execution
* **Makinedeki Etkisi:** Fabrika LAN ağından HMI paneline sızılıp .DXF ve NC kodları değiştirilebilir, yanlış kesim parametreleri yüzünden malzeme fırlaması ve operatör yaralanması riski doğar.

#### **D. Siemens PROFIsafe / Safety PLC Logic**
* **CVE Kodu:** `CVE-2022-38465` (Siemens S7 CPU Cryptographic Key Exposure)
* **Zafiyet Türü:** Donanımsal Şifreleme Anahtarının Ele Geçirilmesi
* **Makinedeki Etkisi:** Profesyonel bir saldırgan PROFIsafe paketlerini dinleyerek kopyalayabilir, ancak fiziksel E-Stop butonunun donanımsal kontağı (Hardwired 24V STO devresi) manipüle edilemez.

---

### 🛡️ 4. Zafiyet Karar Logu ve Tazmin Edici Kontroller (Patch vs. Mitigation)

Endüstriyel makine üreticisi (AES Group) olarak bir zafiyet tespit edildiğinde **doğrudan yama atmak (Direct Patching)** her zaman mümkün değildir. Çünkü CNC hareket kontrolörü veya Safety PLC yazılımına yapılan bir yama, makinenin **CE sertifikasyonunu, ISO 13849-1 PLd doğrulamasını ve eksen interpolasyon hassasiyetini** bozabilir.

Bu nedenle AES Ar-Ge ekibimiz **3 Aşamalı Zafiyet Karar Mekanizması** uygular:

| CVE / Zafiyet | Doğrudan Yama (Patch)? | Neden Doğrudan Yama Atılamıyor? | Uygulanan Tazmin Edici Kontrol (Compensating Control) |
| :--- | :--- | :--- | :--- |
| **CVE-2020-14500** (Secomea RCE) | **EVET (Yama Atıldı)** | Bakım modülü güvenlik bileşenidir; yama makine hareket mekaniğini etkilemez. | Secomea SiteManager OS v9.6'ya yükseltildi. Tünel sadece MFA + Jump Server ile aktif edilir. |
| **CVE-2022-29888** (Osai VNC) | **HAYIR (Ertelendi / Mitigate Edildi)** | Osai RT-Linux çekirdeğinin güncellenmesi 80 m/dk Gantry eksen interpolasyon zamanlamasını bozabilir. | VNC (Port 5900) kapatıldı. HMI erişimi şifreli TLS ve IP Beyaz Liste (Whitelisting) kısıtlamasına alındı. |
| **CVE-2023-21554** (Windows HMI) | **EVET (Yama Atıldı)** | Windows 10 IoT LTSC güvenlik güncellemesi otomasyon yazılımını etkilemez. | KB5025221 Windows güvenlik yaması HMI IPC'ye yüklendi. SMBv1 protokolü tamamen kapatıldı. |
| **CVE-2022-38465** (PROFIsafe) | **HAYIR (Mitigate Edildi)** | Safety PLC firmware değişimi CE uygunluk beyanının ve TÜV sertifikasının yenilenmesini gerektirir. | PROFIsafe hattı fiziksel olarak izole edildi. Safety PLC'ye yazma yetkisi donanımsal anahtarla kilitlendi. |

---

### 📜 5. AB Siber Dayanıklılık Yasası (CRA) İmalatçı Yükümlülükleri (Madde 10 & 11)

AES Group olarak, AB pazarına ihraç edilen **AES Extreme Ultra** makinelerinde CRA (EU 2024/2847) uyarınca aşağıdaki yasal imalatçı süreçleri yürütülmektedir:

1. **Dinamik SBOM Takibi:** Makinenin tesliminden itibaren **10 yıl boyunca** tüm yazılım bileşenlerinin SBOM kaydı saklanır ve güncellenir.
2. **24 Saatlik Erken Uyarı Bildirimi (Early Warning):** Makinede aktif olarak istismar edilen kritik bir zafiyet (örneğin Secomea RCE) tespit edildiğinde **24 saat içinde** AB Siber Güvenlik Ajansı'na (ENISA) ve yetkili CSIRT'e bildirim yapılır.
3. **72 Saatlik Olay Bildirimi (Incident Notification):** Zafiyetin detaylı kök neden analizi, etkilenen makineler ve alınan tazmin edici tedbirler **72 saat içinde** resmi makamlara sunulur.
4. **14 Günlük Nihai Rapor (Final Report):** Zafiyeti tamamen kapatan yama veya firmware güncelleme paketinin yayınlanmasıyla süreç tamamlanır.

---

*Bu döküman, AES Extreme Ultra otomasyon hattının imalatçı seviyesindeki siber-fiziksel güvenlik ve zafiyet yönetim mimarisini eksiksiz olarak belgelemektedir.*
