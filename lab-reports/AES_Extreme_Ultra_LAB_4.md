# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## LAB 4 · Secure Remote Access (Güvenli Uzak Erişim) — Özel Çözüm Föyü

---

### **Görev A — Mevcut vs. Hedef Mimari**

* **MEVCUT:** Uzak bakım modülü doğrudan internete açık, ortak admin şifreleri kullanılıyor, oturum kaydı tutulmuyor, bağlantı sürekli açık.
* **HEDEF:** Doğrudan erişim engellenerek **Jump Server, VPN ve MFA** zorunlu kılınır. Ortak hesaplar kapatılarak **kişisel hesaplarla** sadece izin verilen sürelerde (**varsayılan kapalı**) bağlantı sağlanır ve tüm işlemler **oturum kaydı** ile izlenir.

---

### **Görev B — Functional Safety Köprüsü**

1. **Saldırgan tüm önlemlere rağmen içeri girerse emniyet fonksiyonu etkilenir mi? Neden?**
   * **Hayır, etkilenmemelidir.** Çünkü emniyet mimarisi (Safety PLC → STO hattı), uzaktan erişilebilen üretim ve operasyon kontrol ağından tamamen bağımsız çalışan ayrı bir donanımsal ve mantıksal emniyet kulvarındadır.

2. **Işık perdesi ve STO zincirinin uzak bakım yolundan etkilenmemesi için GEREKSİNİM:**
   * *"AES Extreme Ultra CNC hattının emniyet zinciri (Spindle STO + Emniyet Kapıları → Safety PLC), uzaktan erişim sağlanan bakım ve operasyon ağlarından tamamen bağımsız mantıksal ve donanımsal kanalda çalışmalı; dış ağdan gelen hiçbir parametre değişikliği emniyet kilitlenme koşullarını devre dışı bırakamamalıdır."*
