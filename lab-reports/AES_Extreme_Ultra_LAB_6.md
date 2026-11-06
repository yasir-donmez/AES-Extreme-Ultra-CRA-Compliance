# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## LAB 6 · CRA Incident Simulation & Olay Müdahale Prosedürü (Özel Çözüm Föyü)

**Raporu Hazırlayan:** AES Group Ar-Ge ve Otomasyon Mühendisliği Ekibi (İmalatçı Perspektifi)  
**Çıktı:** Incident Workflow (Evidence Pack EP 13 Incident Response)  
**Mevzuat ve Standart Hizalaması:** AB Siber Dayanıklılık Yasası (CRA - EU 2024/2847 Madde 11), AB Makine Tüzüğü (2023/1230 Ek III 1.1.9), ISO/IEC 27035, NIST SP 800-61  

---

### 📌 1. Olay Senaryosu ve Bağlam
* **Tarih / Saat:** 12 Ekim 2026, Saat 10:15.  
* **Olay Tanımı:** AES Extreme Ultra CNC Nesting hattının fabrikadaki Secomea SiteManager 3329 Uzak Bakım Gateway'i üzerinde yetkisiz bir dış IP adresinden aktif oturum açıldığı ve Osai CNC Hareket Kontrolörünün interpolasyon ve Gantry köprü ivmelenme parametrelerinin değiştirilmeye çalışıldığı tespit edilmiştir.  
* **Makine Durumu:** Makine aktif olarak 24.000 RPM Spindle ile MDF plaka kesmektedir. Vardiya sorumlusu tedirgin durumdadır.  
* **Altın Kural:** *"Resetleyip devam edelim"* refleksi, adli kanıtları (RAM, pcap, syslog) ve kök neden analiz izlerini sonsuza dek siler. Önce **EMNİYET VE CAN KORUMASI**, hemen ardından **KANIT İZOLASYONU** sağlanmalıdır.

---

### ⏱️ 2. Zaman Çizelgesi ve Müdahale Adımları (Incident Workflow)

#### **1. 10:15 — İlk 15 Dakika (İlk Müdahale & Triyaj)**
* **Kimi Ararsınız?:**
  1. Fabrika Vardiya Amiri ve OT Ağ Güvenlik Uzmanı.
  2. AES Group Ar-Ge Destek / Siber Müdahale Ekibi.
* **İlk Üç Eylem:**
  1. **Fiziksel Emniyete Alma:** Makine panosundaki E-Stop butonuna basılarak Spindle ve Gantry hareketleri anında **STO (Safe Torque Off)** durumuna çekilir. *(Not: Ahşap tozu birikip patlama riski oluşturmasın diye ATEX havalandırma emiş fanı durdurulmaz!)*
  2. **Fiziksel Ağ İzolasyonu:** Secomea Gateway'in dış internet (WAN) Ethernet kablosu fiziksel olarak sökülür. OT iç ağından makine izole edilir. **PLC ve IPC ASLA RESETLENMEZ!**
  3. **Triage ve Durum Dondurma:** HMI ekran görüntüsü ve aktif alarm kodu kaydedilir; müdahale zaman damgası log defterine yazılır.

#### **2. İlk 2 Saat (Emniyet Güvencesi, Kanıt İzolasyonu & Hesap Kapatma)**
* **Emniyet Güvende mi?:** Siemens S7-1500F Safety PLC'nin TIA Portal checksum değeri kontrol edilir. Emniyet yazılımının kilitli olduğu, ışık perdesi ve kapak kilitlerinin donanımsal olarak bağımsız çalışmaya devam ettiği doğrulanır.
* **Neyi Korumalısınız (Kanıt!):**
  * Secomea Gateway bellek dump'ı ve aktif WAN/LAN paket yakalama (pcap) logları.
  * Windows 10 IoT HMI IPC üzerindeki Event Viewer ve AES TouchHMI kullanıcı erişim logları.
  * Osai CNC NC-code dizinindeki dosya değiştirilme zaman damgaları.
* **Hangi Hesap Kapatılır?:** Zafiyet tespit edilen varsayılan servis hesabı ve Secomea üzerindeki tüm aktif VPN kullanıcı oturumları anında revoke edilir.

#### **3. 24 Saat — CRA Erken Uyarı Bildirimi (Early Warning Notification)**
* **Kapsam:** AB Siber Dayanıklılık Yasası (CRA EU 2024/2847 Madde 11) uyarınca ENISA'ya ve yetkili CSIRT makamına yapılan ilk resmi bildirimdir.
* **Hazır Olması Gereken Bilgiler:**
  * İmalatçı ve Ürün Bilgisi: AES Group — AES Extreme Ultra v4.2 CNC Line.
  * Olay Türü: Yetkisiz Dış Erişim & CNC Hareket Parametresi Manipülasyon Girişimi.
  * Tespit Zamanı: 12 Ekim 2026, 10:15.
  * İlk Etki ve Durum: STO ile makine emniyete alındı, fiziksel yaralanma oluşmadı, dış ağ izolasyonu sağlandı.

#### **4. 72 Saat — CRA Detaylı Olay Bildirimi (Incident Notification)**
* **Hazır Olması Gereken Bilgiler:**
  * **Kök Neden Analizi:** Secomea Gateway firmware'indeki güncellenmemiş CVE-2020-14500 zafiyeti üzerinden yetkisiz oturum elde edildiği anlaşılmıştır.
  * **Etki Değerlendirmesi:** Safety PLC bağımsızlığı sayesinde operatör yaralanması engellenmiştir. Osai CNC interpolasyon parametrelerinde hafif sapma tespit edilmiştir.
  * **Alınan Önlemler:** İzolasyon bölgesinde yama testi tamamlanmış, IP Whitelisting ve Jump Server zorunluluğu aktif edilmiştir.

#### **5. 14 Gün — CRA Nihai Rapor (Final Report & Audit Trail)**
* **Korunmuş Kayıtlar ve Dokümantasyon:**
  * Adli analiz raporu ve kriptografik olarak imzalanmış syslog kayıtları.
  * TIA Portal Safety checksum doğrulama belgesi.
  * Güncellenmiş Secomea Firmware v9.6 doğrulama testi raporu.
* **Süreç Kapanışı:** Tüm etkilenen makinelerde telafi edici kontroller uygulanmış, Risk Register (Evidence Pack EP 04) ve Olay Müdahale Planı (EP 13) güncellenmiştir.

---

### 📋 3. Görev Özeti ve Kanıt Hizalaması
* **Üretilen Çıktı:** *Incident Workflow & CRA Notification Matrix*
* **Kanıt Paketi Karşılığı:** **Evidence Pack EP 13 Incident Response**
