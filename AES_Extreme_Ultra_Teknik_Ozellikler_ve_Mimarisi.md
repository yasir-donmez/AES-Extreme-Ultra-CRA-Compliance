# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## Teknik Özellikler, OT ve Emniyet Mimarisi Dökümanı

---

### 📌 1. Genel Tanım ve Ürün Konumlandırması
**AES Extreme Ultra**, AES Group'un ahşap, kompozit, plastik ve alüminyum panellerin işlenmesi için geliştirdiği, esnek üretim imkânı sunan yüksek hassasiyetli CNC Nesting ve Delik işleme hattıdır. Fiyat/performans oranı, sağlam gantry gövde yapısı ve modüler otomasyon opsiyonlarıyla ahşap işleme ve mobilya imalat sektöründe en çok tercih edilen lokomotif modellerden biridir.

---

### ⚙️ 2. Mekanik Yapı ve Eksen Performansı
* **Gövde Mimarisi:** Yüksek rijitliğe sahip **Gantry Design** (Köprülü gantry yapı).
* **Çalışma Alanı Opsiyonları (Workfields):**
  * Genişlik (Y): 1300 mm, 1600 mm, 2100 mm.
  * Uzunluk (X): 2500 mm, 2800 mm, 3200 mm, 3600 mm, 4200 mm, 5700 mm.
  * Z-Ekseni Çalışma Yüksekliği: 200 mm.
* **Eksen Hızları:**
  * X-Ekseni: **80 m/dk**
  * Y-Ekseni: **80 m/dk**
  * Z-Ekseni: **20 m/dk**
* **Gövde Koruması & Yağlama:**
  * Otomatik Merkezi Yağlama Sistemi (Sürtünmeyi azaltır, arızayı önler).
  * Kapalı Kablo Kanalları (Aggresif ahşap tozlarına ve çapaklara karşı elektronik kabloları korur).
  * Rulman ve kızaklarda ek toz sızdırmazlık contaları.

---

### 🪓 3. Spindle Motoru, Takım Değiştirme ve Delik Grubu
* **Spindle Motor Seçenekleri:**
  * Seramik rulmanlı, hava veya sıvı soğutmalı seçenekler:
    * **9 kW (12 HP), HSK-F63** (24.000 RPM)
    * **12 kW (15 HP), HSK-F63**
    * **14 kW (19 HP), HSK-F63**
* **Takım Değiştirici (Tool Changer):**
  * X ekseni boyunca hareket eden **8, 12 veya 16 pozisyonlu Döner (Rotary) Takım Şarjörü**.
  * Tüm şarjör pozisyonlarında Anti-Crash (Çarpışma Önleme) kontrol sensörleri mevcuttur.
  * Otomatik Takım Boyu Ölçüm Sistemi (Kalibre ölçüm yüzeyi ile gerçek değer karşılaştırılıp kütüphanede otomatik güncellenir).
* **C-Ekseni (Opsiyonel 4. Eksen):**
  * 0° - 360° arası interpolasyonlu otomatik agregat yönlendirme.
* **Delik Ünitesi (Drill Head Options):**
  * **DH10:** 10 dikey spindle
  * **DH17:** 10 dikey, 6 yatay spindle, 1 entegre testere
  * **DH18:** 18 dikey spindle
  * **DH21:** 14 dikey, 6 yatay spindle, 1 entegre testere
  * **DH22:** 12 dikey, 8 yatay spindle, 2 entegre testere

---

### 🌪️ 4. Vakum Tablası ve Talaş Emiş / ATEX Sistemleri
* **High Flow Matrix Grid Tabla:**
  * Aşınmaya dayanıklı HPL (High Pressure Laminate) malzeme, 30x30 mm ızgara yapısı.
  * Parça boyutuna göre **18 bağımsız vakum bölgesine** kadar otomatik bölünebilir yapı.
* **VACUBOOST Akıllı Vakum Sistemi:**
  * Çift vakum pompası mimarisi (140 m³/h, 250 m³/h, 300 m³/h seçenekleri).
  * Birinci pompa parçayı sabit tutarken, ikinci pompa kesici kafanın bulunduğu aktif bölgeye vakumu yoğunlaştırır.
* **Otomatik Kontrollü Talaş Emiş Akış Yönetimi:**
  * Emiş gücünü, çalışan üniteye göre (delik kafası veya freze kafası) otomatik yönlendirir.
  * Pnömatik olarak yüksekliği ayarlanabilir emiş davlumbazı.

---

### 🤖 5. Otomasyon Hat Opsiyonları (Extreme Ultra Line)
* **Otomatik Besleme:** Hidrolik kaldırma tablası ve vakumlu vantuz tutucu yükleme ünitesi.
* **Otomatik Boşaltma:** Kesim sonrası parçaları ve tozu süpüren pushed-off itici ve temizleme ünitesi.
* **Çıkış Konveyörü:** İşlenen parçaları operatöre taşıyan bant sistemi ve entegre barkod/etiket yazıcısı.

---

### 💻 6. Kontrol, Yazılım ve OT Ağ Mimarisi
* **CNC Kontrolör:** Osai CNC Kontrol / AES PLC Eksen Kontrolü.
* **Operatör Arayüzü (HMI):**
  * Elektrik panosuna entegre 21" Dokunmatik Renkli Ekran veya Hareketli Mobil Konsol.
  * LED renkli durum gösterge barları.
  * **Handterminal Pro:** Eksenleri, potansiyometreli hız ayarlarını, vakum bölgelerini ve emniyet stopunu kontrol eden el kumandası.
* **Yazılım & CAD/CAM:**
  * **NC Hops / Alphacam** CAD/CAM entegrasyonu.
  * .DXF, .STL, .STEP formatlarında 3D simülasyon ve çarpışma kontrolü.
  * Barkod tarayıcı ile otomatik program çağırma.

---

### 🛡️ 7. Emniyet ve Siber Güvenlik Mimarisi (Safety 4.0 / IEC 62443 / AB 2023/1230)
* **Fiziksel Emniyet Donanımları:**
  * Işık perdeleri (Light Curtains), Alan Tarayıcılar (Area Scanners) ve emniyet kilitli kapılar.
  * Sensörlü referans dayama silindirleri.
  * Donanımsal Acil Stop Butonları (HMI panosunda, el terminalinde ve makine çevresinde).
* **Safety Function & Safe State:**
  * **STO (Safe Torque Off):** E-Stop veya alan ihlalinde 24.000 RPM Spindle torku ve servo hareketleri anında kesilir.
  * **Koşullu Safe State (ATEX Zone 22):** E-Stop basıldığında talaş emiş havalandırması ve vakum kapatılamaz! Kesim anında askıda kalan ahşap tozunun emilmemesi durumunda Toz Patlaması (Combustible Dust Explosion) riski doğacağı için havalandırma çalışmaya devam eder.
* **Siber Güvenlik & Ağ Mimarisi:**
  * **Uzak Bakım Gateway:** Secomea / Ewon endüstriyel router üzerinden VPN + MFA + Jump Server korumalı güvenli uzak erişim.
  * **Ağ Bölgeleme (IEC 62443):** Safety PLC en izole bölgede (Safety Zone) yer alır; HMI ve uzaktan erişim hatları güvenlik duvarı (Firewall) ile ayrılmıştır.

---
*Bu teknik doküman, AES Extreme Ultra kaynakları ve Safety 4.0 çerçevesi esas alınarak derlenmiştir.*
