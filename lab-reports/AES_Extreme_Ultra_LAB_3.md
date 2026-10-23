# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## LAB 3 · Threat & Risk Register (Risk Kaydı) — Özel Çözüm Föyü

---

### **Risk Kaydı Tablosu (L x S x E Matrisi)**

| # | Senaryo (Kim → Kapı → Eylem → Zincir → Fiziksel Sonuç) | L | S | E | Skor | Öncelik Seviyesi |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **1** | **Fırsatçı Dış Saldırgan** → Secomea uzaktan bakım modülündeki zafiyetten sızar → Safety PLC'deki ışık perdesi durdurma yanıt süresini uzatır → Operatör yükleme yaparken Spindle STO komutu gecikir → **24.000 RPM dönen kafa operatörün elini ve uzvunu koparır.** | 3 | 3 | 3 | **27** | **Kritik (S3)** |
| **2** | **Meraklı İçeriden Çalışan** → HMI web arayüzü veya USB portundan yetkisiz bağlanır → Talaş emiş fanı debisini ve vakum basıncını düşürür → İşleme alanında yüksek miktarda ahşap tozu birikir → **Spindle sürtünme kıvılcımı ile Toz Patlaması (ATEX Zone 22) oluşur, yakındaki operatör şiddetli patlama ve yangında ağır yaralanır.** | 2 | 3 | 2 | **12** | **Yüksek (S3)** |
| **3** | **Tedarik Zinciri Servis Elemanı** → Virüslü laptop ile PLC'ye bağlanır → Yanlış/imzasız firmware yükler → E-Stop yanıt zinciri bozulur → **Müdahale sırasında Gantry köprü hareketi durmaz, teknisyen sıkışarak yaralanır.** | 1 | 3 | 1 | **3** | **Düşük (S3 Bayrağı)** |

*Skor Derecelendirmesi: Kritik (18–27), Yüksek (9–17), Orta (4–8), Düşük (1–3)*

---

### **Görev Soruları Yanıtları**

1. **En Yüksek Öncelikli Senaryo:** **1. Senaryodur (Skor: 27 - Kritik).** Çünkü internete açık kapıdan Safety PLC konfigürasyonunun bozulması hem en kolay (L=3, E=3) hem de uzuv kaybına (S=3) yol açan en tehlikeli yoldur.
2. **S=3 İstisnası:** **Evet, 3. Senaryodur (Skor: 3).** Skoru düşük (L=1, E=1) kalsa da ağır yaralanma (S=3) riski taşıdığından "S=3 Kuralı" gereği risk kaydında yüksek öncelikli emniyet bulgusu olarak öne çıkarılır.
