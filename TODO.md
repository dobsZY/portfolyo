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

## Açık — test bekliyor

- [ ] **Gerçek iPhone'da hero videosu.** Mobilde kaydırmayla tarama açıldı, ama iOS Safari
      duraklatılmış videoda kareyi çizmeme davranışı buradan test edilemiyor. `loadeddata`
      anında tek karelik bir `play()/pause()` ile dekoderi uyandırıyoruz; gerçek cihazda
      tutmazsa `_scrub`'ı iOS'ta kapatmak tek satırlık iş.
- [ ] **Mobil veri.** Tarama dosyanın tamamını gerektiriyor (15 MB). Veri tasarrufu modu ve
      2G/3G bağlantılar otomatik poster'a düşüyor, ama iyi 4G'de 15 MB iniyor. Rahatsız
      ederse: mobil için ayrı, küçük bir kopya servis etmek gerekir (masaüstü kalitesi
      korunur) — ya da mobilde tekrar poster'a dönülür.

## Opsiyonel / sıra bekleyenler

- [ ] 320 px genişlikte (iPhone SE) üst menü hâlâ ~48 px taşıp yatay kayıyor. 375 px ve
      üstünde beş madde de sığıyor. Kabul edilebilir bulundu, istenirse yazı küçültülür.
- [ ] `uploads/islemci-web_2.mp4` faststart değil (`moov` atomu sonda). Kayıpsız remux ilk
      kareyi hızlandırır: `ffmpeg -i in.mp4 -c copy -movflags +faststart out.mp4`
      (makinede ffmpeg kurulu değil)
- [ ] GSAP ve three.js `<script>` etiketlerinde SRI yok. Önce kayan `gsap@3` etiketini
      sabit sürüme çekmek gerekiyor.
- [ ] Tüm içerik client-side render ediliyor; unpkg.com erişilemezse sayfa boş kalıyor.
      Mimari değişiklik, ayrı bir iş.

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
