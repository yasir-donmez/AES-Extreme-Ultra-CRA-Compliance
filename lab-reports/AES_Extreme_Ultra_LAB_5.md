# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## LAB 5 · Zafiyet, Yazılım Envanteri (SBOM) ve Yama Yönetimi

**Hazırlayan:** Yasir Dönmez – 250541120  
**Mevzuat ve Standart Hizalaması:** AB Siber Dayanıklılık Yasası (CRA - EU 2024/2847), AB Makine Tüzüğü (2023/1230), IEC 62443-4-1 / IEC 62443-4-2

---

### 1. Giriş ve Kapsam
Bu döküman, AES Group tarafından üretilen **AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı** üzerinde çalışan tüm gömülü yazılımlar, işletim sistemleri, kontrolör derlemeleri ve dikey entegrasyon yazılımlarının **Yazılım Envanterini (SBOM - Software Bill of Materials)** ve bunlara bağlı **Zafiyet / Yama Yönetim Protokolünü** içerir.

Jenerik "PLC" veya "PC" tanımları yerine; hatta entegre edilen donanım mimarileri, firmware sürümleri, protokol portları ve bilinen güvenlik zafiyetleri (CVE) ayrıntılı biçimde dokümante edilmiştir.

---

### 2. Bileşen Bazlı Detaylı Yazılım Envanteri (SBOM)

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

### 3. CVE Zafiyet Analizi ve Risk Eşleştirmesi

AES Extreme Ultra üzerinde kullanılan endüstriyel bileşenlerin küresel zafiyet veri tabanlarındaki (NVD / CISA KEV) bilinen zafiyetleri ve makine üzerindeki fiziki etkileri aşağıda analiz edilmiştir. CVE eşleştirmeleri NVD ve üretici bültenleriyle doğrulanmıştır. Osai bileşeni için kamuya açık, doğrulanmış bir CVE bulunamadığından o bileşen için genel zafiyet sınıfı verilmiştir.

#### **A. Secomea GateManager / SiteManager Uzak Bakım Altyapısı (Dış Erişim Kapısı)**
* **CVE Kodu:** `CVE-2020-14500` (Secomea GateManager, 9.2c öncesi sürümler)
* **Zafiyet Türü:** Improper Neutralization of Null Byte or NUL Character (CWE-158); doğrulama kontrollerini atlatan negatif değerle rastgele veri üzerine yazma
* **Makinedeki Etkisi:** Uzak bakım altyapısının bütünlüğünü zayıflatır. Bu katman ele geçirilirse saldırgan makinenin iç otomasyon ağına (PROFINET) ulaşma ve HMI yetkilerine, CNC kodlarına müdahale etme imkânı arar.

#### **B. Osai Open-Control CNC Kernel (RTOS)**
* **CVE Kodu:** Spesifik CVE atanmamıştır; genel zafiyet sınıfı: kimlik doğrulamasız VNC ve Telnet erişimi
* **Zafiyet Türü:** Yetkisiz Erişim ve Kimlik Doğrulama Baypası
* **Makinedeki Etkisi:** Port 5900 (VNC) veya Port 23 (Telnet) üzerinden şifresiz bağlantı sağlanarak Spindle 24.000 RPM dönerken Gantry eksen hızları (80 m/dk) aniden değiştirilebilir, takım çarpışmasına (Anti-Crash sensörü baypası) yol açılabilir.

#### **C. Windows 10 IoT HMI & Network Share (SMB)**
* **CVE Kodu:** `CVE-2023-21554` (QueueJumper) / `CVE-2020-0796` (SMBGhost)
* **Zafiyet Türü:** Windows MSMQ ve SMB Remote Code Execution
* **Makinedeki Etkisi:** Fabrika LAN ağından HMI paneline sızılıp .DXF ve NC kodları değiştirilebilir, yanlış kesim parametreleri yüzünden malzeme fırlaması ve operatör yaralanması riski doğar.

#### **D. Siemens PROFIsafe / Safety PLC Logic**
* **CVE Kodu:** `CVE-2022-38465` (Siemens SIMATIC S7-1500 CPU, V2.9.2 öncesi; SSA-568427)
* **Zafiyet Türü:** Yetersiz Korunan Global Özel Anahtar (CWE-522)
* **Makinedeki Etkisi:** Saldırgan tek bir CPU üzerinde çevrimdışı analizle global özel anahtarı çıkarıp korumalı yapılandırma verisini çözebilir ve eski PG/PC ve HMI iletişimini taklit edebilir. Ancak fiziksel E-Stop butonunun donanımsal kontağı (Hardwired 24V STO devresi) manipüle edilemez.

---

### 4. Zafiyet Karar Logu ve Tazmin Edici Kontroller (Patch vs. Mitigation)

Endüstriyel makinelerde bir zafiyet tespit edildiğinde **doğrudan yama atmak (Direct Patching)** her zaman mümkün değildir. Çünkü CNC hareket kontrolörü veya Safety PLC yazılımına yapılan bir yama, makinenin **CE sertifikasyonunu, ISO 13849-1 PLd doğrulamasını ve eksen interpolasyon hassasiyetini** bozabilir.

Bu nedenle her zafiyet için yama uygulanabilirliği değerlendirilir ve gerekirse tazmin edici kontrol devreye alınır:

| CVE / Zafiyet | Doğrudan Yama (Patch)? | Neden Doğrudan Yama Atılamıyor? | Uygulanan Tazmin Edici Kontrol (Compensating Control) |
| :--- | :--- | :--- | :--- |
| **CVE-2020-14500** (Secomea GateManager) | **EVET (Yama Atıldı)** | Bakım modülü güvenlik bileşenidir; yama makine hareket mekaniğini etkilemez. | Secomea bileşenleri v9.6'ya yükseltildi (9.2c öncesi sürümler etkilenir). Tünel sadece MFA + Jump Server ile aktif edilir. |
| **Osai VNC / Telnet** (genel zafiyet sınıfı) | **HAYIR (Ertelendi / Mitigate Edildi)** | Osai RT-Linux çekirdeğinin güncellenmesi 80 m/dk Gantry eksen interpolasyon zamanlamasını bozabilir. | VNC (Port 5900) ve Telnet (Port 23) kapatıldı. HMI erişimi şifreli TLS ve IP Beyaz Liste (Whitelisting) kısıtlamasına alındı. |
| **CVE-2023-21554** (Windows HMI) | **EVET (Yama Atıldı)** | Windows 10 IoT LTSC güvenlik güncellemesi otomasyon yazılımını etkilemez. | KB5025221 Windows güvenlik yaması HMI IPC'ye yüklendi. SMBv1 protokolü tamamen kapatıldı. |
| **CVE-2022-38465** (Siemens S7-1500) | **HAYIR (Mitigate Edildi)** | Sahadaki eski firmware'li (V2.9.2 öncesi) Safety PLC'lerde güncelleme, CE uygunluk beyanının ve TÜV sertifikasının yenilenmesini gerektirir. | PROFIsafe hattı fiziksel olarak izole edildi. Safety PLC'ye yazma yetkisi donanımsal anahtarla kilitlendi. Referans yapılandırmadaki v2.9.4 bu zafiyetten etkilenmez. |

---

### 5. AB Siber Dayanıklılık Yasası (CRA) İmalatçı Yükümlülükleri (Madde 13 & 14)

AB pazarına ihraç edilen **AES Extreme Ultra** makineleri için CRA (EU 2024/2847) uyarınca aşağıdaki süreçler öngörülmektedir:

1. **Dinamik SBOM Takibi:** SBOM, teknik dokümantasyonun parçası olarak güncel tutulur. Dokümantasyon, ürünün piyasaya arzından itibaren 10 yıl veya destek süresi (hangisi daha uzunsa) boyunca saklanır (Madde 13).
2. **24 Saatlik Erken Uyarı Bildirimi (Early Warning):** Makinede aktif olarak istismar edilen bir zafiyet (örneğin Secomea tarafında) fark edildiğinde **en geç 24 saat içinde** koordinatör CSIRT'e ve ENISA'ya erken uyarı iletilir (Madde 14).
3. **72 Saatlik Zafiyet Bildirimi (Vulnerability Notification):** Zafiyetin niteliği, etkilenen ürünler ve alınan düzeltici/azaltıcı tedbirler **72 saat içinde** bildirilir (Madde 14).
4. **14 Günlük Nihai Rapor (Final Report):** Aktif istismar edilen zafiyetler için nihai rapor, düzeltici veya azaltıcı önlem kullanıma sunulduktan sonra **en geç 14 gün içinde** sunulur (Madde 14).
