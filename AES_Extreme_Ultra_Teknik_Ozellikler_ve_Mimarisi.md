# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## Teknik Özellikler, OT ve Emniyet Mimarisi Dökümanı

---

### 📌 1. Genel Tanım ve Ürün Konumlandırması
**AES Extreme Ultra**, AES Group'un ahşap, kompozit, plastik ve alüminyum panellerin işlenmesi için geliştirdiği, esnek üretim imkânı sunan yüksek hassasiyetli CNC Nesting ve Delik işleme hattıdır [21, 25]. Fiyat/performans oranı, sağlam gantry gövde yapısı ve modüler otomasyon opsiyonlarıyla ahşap işleme ve mobilya imalat sektöründe en çok tercih edilen lokomotif modellerden biridir [21, 27].

---

### ⚙️ 2. Mekanik Yapı ve Eksen Performansı
* **Gövde Mimarisi:** Yüksek rijitliğe sahip **Gantry Design** (Köprülü gantry yapı) [27, 28].
* **Çalışma Alanı Opsiyonları (Workfields):**
  * Genişlik (Y): 1300 mm, 1600 mm, 2100 mm [28].
  * Uzunluk (X): 2500 mm, 2800 mm, 3200 mm, 3600 mm, 4200 mm, 5700 mm [28].
  * Z-Ekseni Çalışma Yüksekliği: 200 mm [28].
* **Eksen Hızları:**
  * X-Ekseni: **80 m/dk** [28]
  * Y-Ekseni: **80 m/dk** [28]
  * Z-Ekseni: **20 m/dk** [28]
* **Gövde Koruması & Yağlama:**
  * Otomatik Merkezi Yağlama Sistemi (Sürtünmeyi azaltır, arızayı önler) [27, 29].
  * Kapalı Kablo Kanalları (Aggresif ahşap tozlarına ve çapaklara karşı elektronik kabloları korur) [38].
  * Rulman ve kızaklarda ek toz sızdırmazlık contaları [39].

---

### 🪓 3. Spindle Motoru, Takım Değiştirme ve Delik Grubu
* **Spindle Motor Seçenekleri:**
  * Seramik rulmanlı, hava veya sıvı soğutmalı seçenekler [30]:
    * **9 kW (12 HP), HSK-F63** (24.000 RPM) [22, 31]
    * **12 kW (15 HP), HSK-F63** [31]
    * **14 kW (19 HP), HSK-F63** [31]
* **Takım Değiştirici (Tool Changer):**
  * X ekseni boyunca hareket eden **8, 12 veya 16 pozisyonlu Döner (Rotary) Takım Şarjörü** [31].
  * Tüm şarjör pozisyonlarında Anti-Crash (Çarpışma Önleme) kontrol sensörleri mevcuttur [31].
  * Otomatik Takım Boyu Ölçüm Sistemi (Kalibre ölçüm yüzeyi ile gerçek değer karşılaştırılıp kütüphanede otomatik güncellenir) [27, 35].
* **C-Ekseni (Opsiyonel 4. Eksen):**
  * 0° - 360° arası interpolasyonlu otomatik agregat yönlendirme [40].
* **Delik Ünitesi (Drill Head Options):**
  * **DH10:** 10 dikey spindle [32]
  * **DH17:** 10 dikey, 6 yatay spindle, 1 entegre testere [32]
  * **DH18:** 18 dikey spindle [32]
  * **DH21:** 14 dikey, 6 yatay spindle, 1 entegre testere [32]
  * **DH22:** 12 dikey, 8 yatay spindle, 2 entegre testere [32]

---

### 🌪️ 4. Vakum Tablası ve Talaş Emiş / ATEX Sistemleri
* **High Flow Matrix Grid Tabla:**
  * Aşınmaya dayanıklı HPL (High Pressure Laminate) malzeme, 30x30 mm ızgara yapısı [33].
  * Parça boyutuna göre **18 bağımsız vakum bölgesine** kadar otomatik bölünebilir yapı [27, 34, 36].
* **VACUBOOST Akıllı Vakum Sistemi:**
  * Çift vakum pompası mimarisi (140 m³/h, 250 m³/h, 300 m³/h seçenekleri) [35, 36].
  * Birinci pompa parçayı sabit tutarken, ikinci pompa kesici kafanın bulunduğu aktif bölgeye vakumu yoğunlaştırır [36].
* **Otomatik Kontrollü Talaş Emiş Akış Yönetimi:**
  * Emiş gücünü, çalışan üniteye göre (delik kafası veya freze kafası) otomatik yönlendirir [33].
  * Pnömatik olarak yüksekliği ayarlanabilir emiş davlumbazı [31].

---

### 🤖 5. Otomasyon Hat Opsiyonları (Extreme Ultra Line)
* **Otomatik Besleme:** Hidrolik kaldırma tablası ve vakumlu vantuz tutucu yükleme ünitesi [25, 42].
* **Otomatik Boşaltma:** Kesim sonrası parçaları ve tozu süpüren pushed-off itici ve temizleme ünitesi [42].
* **Çıkış Konveyörü:** İşlenen parçaları operatöre taşıyan bant sistemi ve entegre barkod/etiket yazıcısı [42, 43].

---

### 💻 6. Kontrol, Yazılım ve OT Ağ Mimarisi
* **CNC Kontrolör:** Osai CNC Kontrol / AES PLC Eksen Kontrolü [24, 37].
* **Operatör Arayüzü (HMI):**
  * Elektrik panosuna entegre 21" Dokunmatik Renkli Ekran veya Hareketli Mobil Konsol [34, 35, 38].
  * LED renkli durum gösterge barları [35].
  * **Handterminal Pro:** Eksenleri, potansiyometreli hız ayarlarını, vakum bölgelerini ve emniyet stopunu kontrol eden el kumandası [29, 30].
* **Yazılım & CAD/CAM:**
  * **NC Hops / Alphacam** CAD/CAM entegrasyonu [24, 37].
  * .DXF, .STL, .STEP formatlarında 3D simülasyon ve çarpışma kontrolü [37].
  * Barkod tarayıcı ile otomatik program çağırma [39].

---

### 🛡️ 7. Emniyet ve Siber Güvenlik Mimarisi (Safety 4.0 / IEC 62443 / AB 2023/1230)
* **Fiziksel Emniyet Donanımları:**
  * Işık perdeleri (Light Curtains), Alan Tarayıcılar (Area Scanners) ve emniyet kilitli kapılar [40, 41].
  * Sensörlü referans dayama silindirleri [37].
  * Donanımsal Acil Stop Butonları (HMI panosunda, el terminalinde ve makine çevresinde) [29, 30].
* **Safety Function & Safe State:**
  * **STO (Safe Torque Off):** E-Stop veya alan ihlalinde 24.000 RPM Spindle torku ve servo hareketleri anında kesilir [1, 17].
  * **Koşullu Safe State (ATEX Zone 22):** E-Stop basıldığında talaş emiş havalandırması ve vakum kapatılamaz! Kesim anında askıda kalan ahşap tozunun emilmemesi durumunda Toz Patlaması (Combustible Dust Explosion) riski doğacağı için havalandırma çalışmaya devam eder [17, 55].
* **Siber Güvenlik & Ağ Mimarisi:**
  * **Uzak Bakım Gateway:** Secomea / Ewon endüstriyel router üzerinden VPN + MFA + Jump Server korumalı güvenli uzak erişim [13, 24].
  * **Ağ Bölgeleme (IEC 62443):** Safety PLC en izole bölgede (Safety Zone) yer alır; HMI ve uzaktan erişim hatları güvenlik duvarı (Firewall) ile ayrılmıştır [13, 18].

---
*Bu teknik doküman, AES Extreme Ultra kaynakları ve Safety 4.0 çerçevesi esas alınarak derlenmiştir.*
