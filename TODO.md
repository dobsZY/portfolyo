# Yapılacaklar

## Yarın konuşulacak

### 1. E-posta altyapısı — `info@` olarak gönderim

**Durum:** Site artık her yerde `info@dogukanyazici.com` gösteriyor, form da FormSubmit'in
hash'li endpoint'i üzerinden oraya gidiyor. Alma tarafı ImprovMX **ücretsiz** planıyla
gmail'e yönleniyor ve çalışıyor.

**Boşluk:** ImprovMX ücretsiz planda SMTP gönderimi yok (0 gönderim). Yani gelen bir mesajı
Gmail'den cevapladığında karşı taraf cevabı `dogukaanyazici@gmail.com`'dan görüyor —
sitede gmail'i temizlemenin etkisi ilk cevapta kayboluyor.

**Seçenekler:**

| Seçenek | Maliyet | `info@` ile gönderim | Not |
|---|---|---|---|
| Şimdiki durum (ImprovMX free) | 0 | ✗ | Sadece alır |
| Zoho Mail free | 0 | ✓ | 1 alan adı, 5 GB. IMAP/POP yok → Gmail'e bağlanmaz, Zoho webmail/mobil |
| Güzel Hosting kurumsal kutu | ~11–21 TL/ay (doğrulanacak) | ✓ | Tam IMAP/SMTP, Gmail'e "Send mail as" ile bağlanır |
| ImprovMX Premium | 9 $/ay | ✓ | Aynı işi TL fiyatının kat kat üstüne yapar |

**Karar öncesi doğrulanacak:**
- Güzel Hosting'de **tek kutu** fiyatı — ilan edilen 11,53 TL toplu alım fiyatı, sepette
  daha yüksek çıkabilir (sayfadaki yıldızlı not).
- **Yenileme** fiyatı — üstü çizili rakamlar ilk dönem kampanyası olabilir.
- Kutu alınırsa MX kaydı hosting'e geçer → **ImprovMX yönlendirmesi devre dışı kalır**.
  Gmail'de çalışmaya devam etmek için kutunun panelinden gmail'e forward kuralı açılmalı.

**Kodda değişecek bir şey yok** — adres aynı kalıyor, sadece arkasındaki altyapı değişiyor.

### 2. Mobil taraf

Kapsam henüz netleşmedi, konuşulacak. 2026-08-12 kod incelemesinde göze çarpan, gözden
geçirilmeye değer noktalar (hiçbiri doğrulanmış hata değil, mobil viewport'ta test
edilmedi):

- `_mobile` eşiği `(max-width: 760px), (pointer: coarse)`. `pointer: coarse` dokunmatik
  ekranlı büyük cihazları da yakalıyor → 1400 px'lik dokunmatik bir laptopta hero videosu
  taranmıyor, sadece poster görünüyor. Kasıtlı mı, gözden mi kaçtı?
- Mobilde hero 250vh ve video yerine poster. Poster tek başına yeterince iyi duruyor mu?
- PCB WebGL katmanı hero geçildikten sonra mobilde de çalışıyor — batarya açısından
  bakılabilir.
- Lab bölümü telefonda: 620×380 canvas üzerinde saf JS konvolüsyon. Performans ve
  dokunmatik kullanım (sürükle-bırak yerine dosya seçici) test edilmeli.
- `data-wide` işaretli öğeler 860 px altında gizleniyor — header'daki E-POSTA butonu ve
  başlık altı satırı dahil. Mobilde header'da yalnızca "CV ↓" kalıyor.
- Bento grid 640 px altında tek sütuna düşüyor; kartların okunabilirliği kontrol edilmeli.

## Deploy sonrası — unutma

- [ ] Canlı siteden bir test mesajı gönder. FormSubmit aktivasyonu **origin bazlı**;
      `localhost:3000` onaylandı ama `dogukanyazici.com` için ayrı bir "Activate FormSubmit"
      maili gelecek. Onaylanana kadar ziyaretçi "Gönderilemedi" görür.

## Opsiyonel / sıra bekleyenler

- [ ] `uploads/islemci-web_2.mp4` faststart değil (`moov` atomu sonda). Kayıpsız remux ilk
      kareyi hızlandırır, kaliteye dokunmaz:
      `ffmpeg -i in.mp4 -c copy -movflags +faststart out.mp4` (makinede ffmpeg kurulu değil)
- [ ] GSAP ve three.js `<script>` etiketlerinde SRI yok. Eklemek için önce kayan `gsap@3`
      etiketini sabit sürüme çekmek gerekiyor.
- [ ] Tüm içerik client-side render ediliyor; unpkg.com erişilemezse sayfa boş kalıyor.
      Çözümü mimari değişiklik, ayrı bir iş.
