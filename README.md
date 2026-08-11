# Portfolyo

Doğukaan Yazıcı — Yapay Zekâ / Görüntü İşleme Mühendisi.

Tek dosya, kaydırmaya bağlı WebGL sahnesi, tarayıcıda çalışan görüntü işleme demosu.

## Yerelde çalıştırma

```
npx serve .
```

Ana dosya: `index.html` — sitenin tek kaynağı, Vercel de bunu servis eder.
`support.js` DC çalışma zamanıdır ve otomatik yüklenir.

Hero videosu (`uploads/islemci-web_2.mp4`) kaydırmaya bağlı olarak taranır. Sunucu HTTP
Range destekliyorsa tarayıcı dosyayı akıtarak açar; desteklemiyorsa tamamı indirilip
blob'a alınır. `npx serve` ve Vercel Range destekler, `python -m http.server` desteklemez.
