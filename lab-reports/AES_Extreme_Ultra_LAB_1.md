# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## LAB 1 · Safety Architecture (Emniyet Mimarisi) — Özel Çözüm Föyü

---

### **1. Bu makinede tehlike nedir? İnsan neyden zarar görür?**
* **Mekanik Tehlike:** 24.000 RPM hızla dönen 9 kW / 12 kW / 14 kW HSK-F63 Spindle motoru, DH10/DH17/DH21/DH22 çoklu delik kafası ve X/Y eksenlerinde **80 m/dk** hızla hareket eden ağır Gantry köprüsünün çarpması, kesmesi ve uzuv koparması.
* **Proses / Patlama Tehlikesi (ATEX Zone 22):** MDF ve sunta plakaların işlenmesi esnasında oluşan yüksek miktardaki yanıcı ahşap tozları (**Combustible Wood Dust**). Emiş durduğunda kapalı alanda biriken bu tozlar, statik kıvılcım veya sürtünmeyle **Toz Patlamasına** ve yangına yol açarak insana ölümcül zarar verir.

### **2. Safety function (emniyet fonksiyonu) hangisidir?**
* Işık perdesi / alan tarayıcı ihlali veya E-Stop butonuna basılması durumunda Spindle ve Servo motor torkunun anında kesilmesi (**STO - Safe Torque Off**) ve pnömatik kilitli muhafaza kapaklarının kilitlenerek tehlikeli alana erişimin engellenmesidir.

### **3. Safety-related control system nerede?**
* E-Stop Butonu + Işık Perdesi / Emniyet Kapısı Sviçi → **Safety PLC** (SICK / Siemens Safety / Pilz) → **STO Sürücü Girişi (VFD Servo Inverter)** ve Ana Güç Kontaktörleri hattındadır.

### **4. Normal PLC ile Safety PLC farkı nedir?**
* **Normal PLC (Osai CNC / AES PLC):** Üretim akışını, NC kodlarını, vakum vanalarını yönetir. Tek kanallıdır, kilitlenebilir veya yazılımsal olarak baypas edilebilir.
* **Safety PLC:** Çift kanallı (Redundant 1Oo2/2Oo2) mimariye, donanımsal öz denetime (Self-Diagnostic), SIL 2 / SIL 3 - PLd / PLe sertifikasına ve siber müdahalelere karşı kilitli hafızaya sahiptir.

### **5. PLr / SIL neden var? Bu fonksiyon için neden önemli?**
* 24.000 RPM kesici kafa ve 80 m/dk Gantry köprüsü kalıcı uzuv kaybı ve ölüm riski taşıdığı için gerekli performans seviyesi **PLd / PLe (SIL 2 / SIL 3)** olarak belirlenmiştir. Tek bir bileşen arızasında veya siber parametre değişikliğinde emniyetin kilitli kalmamasını garanti eder.

### **6. Safe state (güvenli durum) nedir? (Koşullu Safe State Kriteri)**
* Spindle torku ve Servo hareketleri STO ile anında durdurulur. **ANCAK Yüksek Güçlü Talaş Emiş Fanı ve Vakum Sistemi KÖRLÜKLE KAPATILAMAZ!** Kesim anında askıda kalan ahşap tozunun emilmesi durdurulursa kapalı alanda biriken toz patlayıcı ortam (ATEX Zone 22) oluşturacağı için havalandırma fanı "Koşullu Safe State" gereği çalışmaya devam etmek zorundadır.

### **7. Safety function hangi dijital bağımlılıklara sahip?**
* Safety PLC konfigürasyon parametrelerine, PROFIsafe / PROFINET bus iletişimine ve uzak bakım modülü üzerinden erişilen güvenlik zamanlama parametrelerine (Safety Response Time) bağımlıdır.

### **8. Siber müdahale hangi noktadan bu fonksiyonu bozar?**
* Uzak bakım modülü (Secomea/Ewon) üzerinden Safety PLC yazılımına sızılıp ışık perdesi tepki süresinin uzatılması veya STO mantık bloklarının baypas edilmesi noktasında bozar.
