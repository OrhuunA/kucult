# Küçült

Görselleri toplu küçülten ve sıkıştıran tek dosyalık web aracı. Kurulum yok, sunucu yok, bağımlılık yok — `index.html` dosyasını tarayıcıda açman yeterli.

Tüm işlem tarayıcıda (`canvas.toBlob`) yapılır; **hiçbir dosya sunucuya yüklenmez.**

## Özellikler

- Sürükle-bırak ya da dosya seçerek toplu yükleme
- Çıktı biçimi: WebP · JPEG · PNG
- Kalite ayarı (0,30 – 1,00) ve en fazla genişlik (orijinal / 2560 / 1920 / 1280 / 800 px)
- Her görsel için önce/sonra boyut, yeni çözünürlük ve kazanç yüzdesi
- Önce/sonra kaydırmalı karşılaştırma önizlemesi (her görsel için "Karşılaştır")
- Sürükleyerek yeniden sıralama ve tek tek dosya silme
- Toplam tasarruf özeti
- Tek tek indirme ya da tümünü ZIP olarak indirme
- EXIF dönme bilgisi uygulanır, konum gibi diğer EXIF verileri çıktıya taşınmaz
- Açılışta iki örnek görselle çalışır durumda gelir

## Kullanım

```bash
git clone https://github.com/<kullanici>/kucult.git
cd kucult
# index.html dosyasını tarayıcıda aç — hepsi bu
```

### GitHub Pages'te yayınlamak

Repo ayarlarından **Settings → Pages → Source: Deploy from a branch → main / (root)** seç.
Birkaç dakika içinde `https://<kullanici>.github.io/kucult/` adresinde canlı olur.

## Teknik notlar

- Görsel `createImageBitmap` ile çözülür (`imageOrientation: "from-image"`), canvas'a ölçeklenerek çizilir ve seçilen biçimde yeniden kodlanır.
- JPEG şeffaflığı desteklemez; şeffaf alanlar beyaza boyanır. Şeffaflık gerekiyorsa WebP veya PNG kullan.
- PNG kayıpsız kodlanır, kalite ayarı uygulanmaz — kazanç yalnızca ölçeklemeden gelir.
- Aynı anda en fazla 2 görsel işlenir, böylece büyük partilerde arayüz donmaz.
- Karşılaştırma önizlemesi, orijinal ve küçültülmüş görseli aynı çerçevede üst üste bindirip `clip-path` ile kaydırmalı olarak açar; fare/dokunma sürüklemesi ve kaydırıcı (range input) birlikte çalışır.
- Sıralama, satır başındaki tutamaçtan native HTML5 sürükle-bırak (`dragstart`/`dragover`/`drop`) ile yapılır; silme, listeden ve bellekten (object URL'ler dahil) kaldırır.
- Tek dış bağımlılık ZIP indirme için CDN'den yüklenen [JSZip](https://stuk.github.io/jszip/) 3.10.1'dir; yüklenemezse tek tek indirme çalışmaya devam eder.

## Yol haritası

- [x] Sürükleyerek sıralama ve tek tek dosya silme
- [x] Önce/sonra karşılaştırma önizlemesi (kaydırmalı)
- [ ] AVIF çıktısı (destekleyen tarayıcılarda)
- [ ] Web Worker'a taşıyıp büyük partilerde tam akıcılık

## Lisans

MIT
