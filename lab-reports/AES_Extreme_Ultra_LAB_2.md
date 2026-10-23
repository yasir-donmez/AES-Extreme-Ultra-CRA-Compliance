# AES Extreme Ultra CNC Nesting & Delik Otomasyon Hattı
## LAB 2 · IEC 62443 Zone & Conduit (Ağ Bölgeleme) — Özel Çözüm Föyü

---

### **Görev A — Varlıkları Bölgelere Ayırma**

#### **1. Bölge Gruplandırması:**
* **Safety Zone (Emniyet Bölgesi):** Safety PLC, STO Sürücü Girişleri, Emniyet I/O Modülleri, PROFIsafe bus.
* **Machine Control Zone (Saha Kontrol Bölgesi):** Üretim PLC (Osai CNC / AES PLC), VFD Servo Sürücüler, Pnömatik Vakum Vanaları, PROFINET.
* **Operations Zone (Operasyon Bölgesi):** 21" Industrial HMI (VNC/HTTP web arayüzlü), Handterminal Pro.
* **External / Remote Access Zone (Dış Erişim Bölgesi):** Secomea/Ewon Uzak Bakım Modülü, CAD/CAM (Alphacam/NC Hops) Fabrika Ağ Bağlantısı, Wi-Fi AP, USB Portları.

#### **2. Açık Uzak Bakım Modülü Analizi:**
* Dış Erişim Bölgesindedir ve doğrudan Saha/Emniyet Bölgesinde **KALAMAZ**.
* **Nedeni:** İnternete açık bir geçidin iç otomasyon ağında kalması, siber saldırganın hiçbir engelle karşılaşmadan doğrudan PLC'lere erişip makine parametrelerini değiştirmesine yol açar. Arada DMZ ve Firewall zorunludur.

#### **3. Bölgeler Arası Geçişler (Conduits):**
* **Conduit 1 (Dış Erişim ↔ DMZ):** Firewall, VPN tüneli ve MFA ile kimlik doğrulama süzülür.
* **Conduit 2 (HMI ↔ Saha Kontrol):** Şifresiz HTTP trafiği ve yetkisiz VNC bağlantıları kısıtlanır.
* **Conduit 3 (Saha Kontrol ↔ Safety Zone):** Yalnızca kısıtlı Read-Only PROFIsafe trafiğine izin verilir.

---

### **Görev B — Uzak Erişim Karar Tablosu**

| Karar | Seçenekler | Seçiminiz + Nedeni |
| :--- | :--- | :--- |
| **Aracı?** | Doğrudan / Jump server | **Jump server:** Makineye doğrudan bağlantı engellenir; izole ara sunucudan geçilir. |
| **Tünel?** | Açık / VPN | **VPN:** Veri trafiğinin dinlenmesini önlemek için şifreli tünel şarttır. |
| **Kimlik?** | Parola / MFA | **MFA:** Parola çalınmasına karşı çok faktörlü doğrulama zorunludur. |
| **Hesap?** | Paylaşılan / Kişisel | **Kişisel hesap:** Ortak admin hesabı kapatılır; bireysel izlenebilirlik sağlanır. |
| **Kayıt?** | Yok / Tam oturum kaydı | **Tam oturum kaydı:** Olay incelemesi ve adli analiz için tüm işlemler kaydedilir. |
| **Zamanlama?**| Sürekli açık / Varsayılan kapalı | **Varsayılan kapalı:** Bağlantı sürekli değil, sadece onaylı bakım süresince açılır. |
