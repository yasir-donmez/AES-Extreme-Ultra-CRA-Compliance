# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## LAB 7 · AI Safety Challenge & Yapay Zekâ Güvenişim Mimarisi (Özel Çözüm Föyü)

**Raporu Hazırlayan:** AES Group Ar-Ge ve Otomasyon Mühendisliği Ekibi (İmalatçı Perspektifi)  
**Çıktı:** AI Fail-Safe Decision (Evidence Pack EP 15 Verification/Test & AI Governance)  
**Mevzuat ve Standart Hizalaması:** AB Yapay Zekâ Yasası (EU AI Act - High-Risk Industrial AI), ISO/IEC 42001 (AI Management System), ISO 13849-1, IEC 61508  

---

### 📌 1. Temel İlke: Prediction ≠ Safety (Tahmin Emniyet Değildir)
Yapay zekâ (AI/ML) modelleri veri üzerinden **olasılık ve tahmin** üretir (Plaka nesting verimliliği, Akıllı Talaş Emiş Debisi, Kamera Tabanlı Plaka Hizalama, Kestirimci Spindle Titreşim Analizi). **Emniyeti garanti eden mimari ise YZ'nin DIŞINDA, bağımsız ve deterministik donanımda (Safety PLC + STO) tanımlanmalıdır!**

---

### 🔄 2. Sistem Mimarisi ve Veri Akışı
`KaVision Optik Kamera / Titreşim Sensörü` → `AES AI Optimizasyon Servisi (IPC)` → `OK / RED / Parametre` → `Osai CNC Motion Controller` → `Spindle Motor & Servo Sürücüler (STO Korumalı)`

---

### 🛠️ 3. Üç Başarısızlık Senaryosunda Güvenli Davranış (AI Fail-Safe Decisions)

#### **1. Senaryo 1 — Model Yanlış Sınıflandırdı (False Positive / False Negative)**
* **Olay:** Yapay zekâlı görsel malzeme analiz modeli, MDF plakanın kalınlığını ve sertliğini yanlış algılayarak Spindle ilerleme hızını (Feed Rate) 80 m/dk seviyesine ve kesim torkunu aşırı yüksek seviyeye çıkardı.
* **Güvenli Davranış (Deterministic Hard-Limit & Independent Boundary):**
  * YZ modeli Osai CNC'ye ne kadar yüksek hız veya tork komutu gönderirse göndersin, Osai CNC üzerindeki **Donanımsal Hard-Limit** ve VFD sürücü tork sınırları aşılamaz.
  * VFD sürücü akımı %110 sınırını geçtiği an Osai CNC YZ komutunu otomatik olarak geçersiz kılar (Override Reject) ve makineyi emniyetli kesim hızına (Safe Feed Rate) düşürür.

#### **2. Senaryo 2 — Girdi Manipüle Edildi / Sensör Bozuldu (Adversarial / Corrupted Input)**
* **Olay:** Talaş emiş hattındaki optik toz yoğunluk kamerası ahşap tozuyla kaplandı veya kamera verisi şebeke gürültüsüyle bozuldu. YZ modeli ortamda toz olmadığını varsayıp talaş emiş fanını kapatmaya çalıştı.
* **Güvenli Davranış (Input Integrity Check & ATEX Safe Fallback State):**
  * Girdi sinyali için Plausibility Check (Mantıklılık Kontrolü) uygulanır. Eğer optik kirlilik oranı %20'yi geçerse veya sensör verisi donanımsal emiş debisiyle çelişirse YZ kararı reddedilir.
  * Havalandırma sistemi otomatik olarak **ATEX Safe Fallback Mode** seviyesine geçer ve talaş emiş fanı %100 kapasitede çalışmaya devam eder (Toz patlaması riski engellenir).

#### **3. Senaryo 3 — Confidence (Güven Skoru) Düştü (Low Confidence Anomaly)**
* **Olay:** Karmaşık bir alüminyum/kompozit panel kesiminde YZ tabanlı Spindle titreşim analiz modeli kararsız kaldı (Güven skoru %62'ye düştü; kabul edilebilir eşik %85).
* **Güvenli Davranış (Confidence Threshold & Human-in-the-Loop Override):**
  * Confidence skoru %85 eşiğinin altına düştüğünde YZ otonom parametre değiştirme yetkisini anında kaybeder.
  * Makine aniden durdurulup üretim aksatılmaz; ancak Gantry köprü hızı %50'ye düşürülür, 21.5" HMI ekranında *"AI Kararsızlığı: Lütfen Takım ve Malzeme Hizalamasını Doğrulayın"* uyarısı çıkarılır ve insan onayı (Human-in-the-Loop) alınana kadar güvenli modda çalışılır.

---

### 📊 4. AI Fail-Safe Decision Karar Tablosu

| Başarısızlık Modu | Kök Neden / Risk | Tanımlanan Güvenli Davranış | Uygulanan Güvenişim Kavramı |
| :--- | :--- | :--- | :--- |
| **Yanlış Sınıflandırma** | YZ aşırı hız/tork üretti | Osai CNC Hard-Limit ve VFD Tork Sınırı devreye girer | **Deterministic Boundary & Hard-Limit** |
| **Girdi Manipülasyonu** | Lens kirliliği / Bozuk sensör | YZ devre dışı bırakılır, talaş emiş %100 fan gücüne geçer | **Input Plausibility & ATEX Safe Fallback** |
| **Düşük Confidence (%62 < %85)** | Model kararsızlığı | Hız %50'ye düşer, HMI'da insan onayı beklenir | **Confidence Threshold & Human-in-the-Loop** |

---

### 📋 5. Görev Özeti ve Kanıt Hizalaması
* **Üretilen Çıktı:** *AI Fail-Safe Decision Matrix & AI Governance Log*
* **Kanıt Paketi Karşılığı:** **Evidence Pack EP 15 Verification/Test & AI Governance**
