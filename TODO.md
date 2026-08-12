# Yapılacaklar

## Ertelendi — 2026-08-12'de "şimdilik böyle kalsın" denildi

### E-posta altyapısı: `info@` olarak gönderim

Mevcut kurulum bırakıldı: ImprovMX ücretsiz plan `info@dogukanyazici.com`'u gmail'e
yönlendiriyor, form da oraya gidiyor. **Alma tarafı sorunsuz.** Tek eksik, Gmail'den
cevap yazınca karşı tarafın cevabı `dogukaanyazici@gmail.com`'dan görmesi — ImprovMX
ücretsiz planda SMTP gönderimi yok.

Zoho ücretsiz plan araştırıldı ve **vazgeçildi**: (a) IMAP/POP içermediği için Gmail'e
bağlanmıyor, yani zaten Gmail'den çıkmayı gerektiriyordu; (b) "available only in select
data centers" notu var, Türkiye'den kayıt ekranında görünmedi.

Tekrar açılırsa seçenekler:

| Seçenek | Gmail'de kalır mı | Maliyet |
|---|---|---|
| Şimdiki durum | ✅ | 0 |
| Zoho Mail Lite (IMAP var) | ✅ | ~1 $/kullanıcı/ay |
| Güzel Hosting kurumsal kutu | ✅ | ~11–21 TL/ay — tek kutu + yenileme fiyatı doğrulanmalı |

Güzel Hosting'in avantajı: alan adı ve DNS zaten orada (NS `*.guzelhosting.com`), MX/SPF/
DKIM ile uğraşmadan panelden kutu açılıyor. Kodda değişecek bir şey yok, adres aynı.

## Açık

- [ ] **CV PDF'i güncellenmeli.** `assets/Dogukaan-Yazici-CV.pdf` hâlâ eski bilgileri
      taşıyor: GPA 3.20 ve lise şehri Ankara. Sitede ikisi de düzeltildi (3.30 / Samsun),
      YÖK programı da "2025 — 2026" oldu. PDF'i yeniden dışa aktarıp aynı dosya adıyla
      `assets/` altına koyman yeterli — cache başlığı bilerek kısa tutuldu, güncelleme
      anında yayına girer.

## Kapatıldı — gerekmediğine karar verildi (2026-08-12)

- **Faststart remux.** Ölçüldü: `moov` atomu sonda olduğu için tarayıcı fazladan bir istek
  yapıyor (canlıda 669→1114 ms). Kazanç ~450 ms, yani 2,8 sn'lik açılışın altıda biri —
  ffmpeg kurup videoyu yeniden üretmeye değmez. **Videoyu başka bir sebeple yeniden export
  edersen `-movflags +faststart` eklemeyi unutma, o zaman bedava gelir.**
- **Mobil için küçük kopya.** 15 MB mutlak olarak çok ama Wi-Fi'da önemsiz, Vercel bant
  genişliğinde sorun değil. Sınırlı veri paketi bir gün sorun olursa ffmpeg'siz ara yol:
  mobilde `preload="auto"` yerine `preload="metadata"` — tarayıcı dosyanın tamamını peşinen
  çekmez, bedeli tarama sırasında takılma riski.

Kalan dış bağımlılıklar — hepsi **isteğe bağlı iyileştirme**, erişilemezse içerik yine
render oluyor: Google Fonts (yedek font devreye girer), jsdelivr'dan GSAP + ScrollTrigger
(animasyon olmaz, içerik görünür kalır) ve three.js (dekoratif anakart katmanı çizilmez).

## Biten

- [x] Hero videosu HTTP Range ile akıyor — canlıda doğrulandı (Vercel 206 dönüyor, video
      ~2,8 sn'de hazır, kalan 12 MB arkada iniyor)
- [x] FormSubmit hash'li endpoint'e geçildi, e-posta kaynak kodda düz metin değil
- [x] Site genelinde adres `info@dogukanyazici.com` olarak birleştirildi
- [x] FormSubmit aktivasyonu
- [x] `main` push edildi, Vercel deploy aldı
- [x] Cache başlıkları: video 1 yıl `immutable`, görseller 1 hafta. **CV PDF'i bilerek
      dışarıda** — dosya adı sabit olduğu için uzun cache eski CV'yi servis ederdi
- [x] Mobil: iOS'un form alanlarında sayfayı zoomlaması (yazı tipi 16 px'e çıkarıldı)
- [x] Mobil: hero yazısı 68vw → 86vw (sağda 30% boş alan kalıyordu)
- [x] Mobil: header iki satır — üstte isim + CV, altta tam genişlikte menü. Beş madde de
      sığıyor (340/347 px), dokunma hedefleri 30 px → 46 px
- [x] Mobil: kaydırmaya bağlı video taraması açıldı (eskiden donmuş poster + ~1900 px ölü
      kaydırma vardı)
- [x] Gerçek iPhone testi — 2026-08-12'de canlıda doğrulandı, sorun çıkmadı. iOS Safari'nin
      duraklatılmış videoda kare çizmeme sorunu için eklenen `loadeddata` + tek karelik
      `play()/pause()` uyandırması işe yaradı
- [x] **unpkg bağımlılığı kaldırıldı.** React + ReactDOM `vendor/` altına alındı,
      `window.__resources` ile runtime oraya yönlendiriliyor. Dosyalar unpkg'den indirildi
      ve SHA-384'leri support.js'in beklediği SRI değerleriyle doğrulandı. Artık unpkg
      erişilemese de sayfa render oluyor
- [x] GSAP `gsap@3` → `gsap@3.15.0` sabitlendi, GSAP/ScrollTrigger/three.js'e SRI +
      crossorigin eklendi
- [x] 320 px'te (iPhone SE) menü iki satıra sarıyor — beş madde de görünür, 46 px dokunma
      hedefleri korunuyor, yatay kaydırma yok. Bedeli: header 172 px (ekranın %25'i).
      Fazla bulunursa 360 px altında menüyü tamamen gizlemek alternatif
- [x] Ağ koruması daraltıldı: `saveData` her cihazda saygı görüyor, ama `effectiveType`
      tahmini yalnızca telefonda dikkate alınıyor — yavaş açılan bir masaüstü oturumu
      "3g" damgası yiyip hero videosunu kaybetmesin diye
