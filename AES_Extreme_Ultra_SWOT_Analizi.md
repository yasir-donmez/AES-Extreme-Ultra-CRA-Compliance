# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## Siber-Fiziksel SWOT Analizi (İmalatçı / AES Group Ar-Ge Perspektifi)

---

### 📌 Giriş ve Stratejik Çerçeve
Bu SWOT analizi, **AES Group Ar-Ge ve Otomasyon Mühendisliği** gözüyle, firmanın lokomotif modeli olan **AES Extreme Ultra** CNC Nesting hattının mekanik gücünü, emniyet mimarisini (Safety 4.0), AB Makine Tüzüğü (EU 2023/1230) ve Siber Dayanıklılık Yasası (CRA) uyumluluğunu değerlendirmek amacıyla hazırlanmıştır.

---

### 🟢 1. Güçlü Yönler (Strengths)

1. **Donanımsal Mekanik ve Eksen Dominasyonu:**
   * Heavy-Duty Gantry gövde yapısı ile X ve Y eksenlerinde **80 m/dk** yüksek hareket hızı ve hassasiyeti.
   * 24.000 RPM HSK-F63 spindle ve esnek delik grubu (DH10–DH22) ile pazarın en geniş işleme kapasitesi.
2. **Bağımsız Emniyet Mimarisi (Functional Safety Isolation):**
   * Fiziksel insan korumasının (Işık Perdesi + Kapak Kilitleri) doğrudan **Safety PLC → STO (Safe Torque Off)** hattı üzerinden yapılması.
   * Siber saldırı altında dahi fiziksel kilitlerin devre dışı kalmaması.
3. **Pazar Liderliği ve Yüksek F/P Oranı:**
   * Türkiye ve küresel pazarda modüler mobilya imalatçılarının en çok tercih ettiği lokomotif nesting modeli olması.
4. **Akıllı Vakum ve Proses Güvenliği:**
   * 18 bağımsız bölgeli VacuBoost matris vakum tablası.
   * Ahşap tozu birikmesini önleyen ve E-Stop durumunda dahi çalışmaya devam eden **Koşullu Safe State** talaş emiş havalandırması (ATEX Zone 22 koruması).

---

### 🔴 2. Zayıf Yönler (Weaknesses)

1. **Genişletilmiş Siber Saldırı Yüzeyi (Attack Surface):**
   * Uzak bakım router'ları (Secomea / Ewon), Cad/Cam yazılım entegrasyonu (Alphacam / NC Hops) ve Otomatik Etiketleme (Label X) nedeniyle siber giriş noktalarının fazlalığı.
2. **Eski/Lokal Ağ Protokolü Bağımlılıkları:**
   * Saha içi HMI iletişiminde ve servis arayüzlerinde kullanılan şifresiz HTTP (port 80) veya varsayılan VNC bağlantılarının varlığı.
3. **Yama Yönetimi Karmaşıklığı (Patch Friction):**
   * Sertifikalı Osai CNC RT-Linux çekirdeğine veya Safety PLC'ye doğrudan yama atmanın CE sertifikasyonunu ve Gantry interpolasyon hassasiyetini bozma riski (Compensating Control ihtiyacı).

---

### 🟡 3. Fırsatlar (Opportunities)

1. **AB Mevzuat Uyumu ile İhracat Avantajı:**
   * AB Makine Tüzüğü (2023/1230) ve CRA gereksinimlerine göre hazırlanan **Denetim Kanıt Paketi (Evidence Pack)** sayesinde Avrupa pazarındaki rakiplere karşı belirgin üstünlük sağlama.
2. **Güvenli Uzak Servis (Cyber-Secured Remote Maintenance):**
   * Müşterilere **Jump Server, VPN ve MFA** korumalı "Güvenli Uzak Bakım Paketleri" sunarak katma değerli servis geliri yaratma.
3. **Yapay Zeka Destekli Kestirimci Bakım (Predictive Maintenance):**
   * Spindle ve VFD verilerini salt-okunur (read-only) ağ üzerinden toplayarak, emniyeti riske atmadan AI destekli kestirimci bakım çözümleri geliştirme.

---

### 🟠 4. Tehditler (Threats)

1. **Tedarik Zinciri ve Firmware Saldırıları:**
   * İkinci taraf VFD sürücülere veya PLC bileşenlerine imzasız/virüslü firmware enjekte edilerek üretim hattının durdurulması veya kilitlenmesi.
2. **ATEX ve Proses Sabotajı Riski:**
   * Siber saldırganın talaş emiş fan debilerini düşürerek işleme alanında ahşap tozu patlaması (ATEX Zone 22) tetikleme riski.
3. **CRA İdari Yaptırımları ve İtibar Kaybı:**
   * AB'ye ihraç edilen makinelerde siber zafiyet veya olay bildirim sürelerinin (24s / 72s / 14 gün) ihlali durumunda uygulanabilecek ağır cezalar ve piyasadan geri çağırma riski.
