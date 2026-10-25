# Gazi Özdemir Okul Takip Sistemi

Bu klasör GitHub deposuna yüklenecek uygulamanın tamamıdır. `public/` arayüzü ve PDF şablonlarını, `server.mjs` uygulama sunucusunu, `lib/gemini.mjs` ise Gemini bağlantısını içerir. Ek paket kurulumu ve derleme gerektirmez.

## Bilgisayarınızda çalıştırma

1. Node.js 22.9 veya daha yeni bir sürüm kurun.
2. Terminalde bu klasöre girin.
3. `.env.example` dosyasını **`.env`** adıyla kopyalayın.
4. `.env` içindeki `GEMINI_API_KEY` alanına kendi Gemini API anahtarınızı yazın. Anahtarı tırnak içinde de yazabilirsiniz. `GEMINI_MODEL` hesabınızda erişilebilir bir model olmalıdır; gerekiyorsa değiştirin.
5. `npm start` komutunu çalıştırın.
6. Tarayıcıda `http://127.0.0.1:4173` adresini açın.

`npm install` gerekmez. Mac/Linux kopyalama komutu: `cp .env.example .env`. Windows PowerShell: `Copy-Item .env.example .env`.

Port doluysa `.env` içindeki `PORT` değerini değiştirin. `.env` değişikliklerinden sonra sunucuyu yeniden başlatın. API anahtarı olmadan arayüz, öğrenci takibi, şablon düzenleme ve PDF indirme çalışır; Gemini düğmesi bağlantının yapılandırılmadığını gösterir.

## GitHub'a yükleme

Yalnızca **bu klasörün içeriğini** yeni deponun köküne yükleyin. `public/`, `lib/`, `test/`, `server.mjs`, `package.json`, `Dockerfile`, `render.yaml`, `README.md`, `.gitignore`, `.dockerignore` ve `.env.example` dosyalarını dahil edin. Gizli dosyalar görünmüyorsa Finder'da Cmd+Shift+. kullanın.

**Gerçek `.env` dosyasını ve API anahtarını GitHub'a yüklemeyin.** `.gitignore` bunu Git ile yüklerken engeller; web arayüzüne sürüklerken `.env` dosyasını kendiniz dışarıda bırakın. Bu pakette gerçek API anahtarı bulunmaz. Kaynak klasöründen `.git`, `.openai` veya `node_modules` kopyalamanız gerekmez.

Örnek komutlar (depo adresini kendi adresinizle değiştirin):

```sh
git init
git add .
git commit -m "Okul takip sistemi ve Gemini proje hazırlama"
git branch -M main
git remote add origin https://github.com/KULLANICI/DEPO.git
git push -u origin main
```

## İnternette çalıştırma

**GitHub Pages bu sunucuyu çalıştırmaz.** Gemini anahtarını korumak için Node.js veya Docker çalıştırabilen bir barındırma hizmeti gerekir. API anahtarını tarayıcı koduna eklemeyin.

### Render ile Docker yayını

1. Klasör içeriğini GitHub deposunun köküne yükleyin.
2. Render'da bu depodan bir Blueprint oluşturun. `render.yaml` Docker sunucusunu tanımlar. Ya da Docker türünde bir Web Service oluşturun.
3. Gizli ortam değişkeni olarak `GEMINI_API_KEY` değerini girin.
4. `GEMINI_MODEL` değerini hesabınızın erişebildiği modele göre ayarlayın.
5. Blueprint, `APP_PASSWORD` için rastgele bir parola üretir. Parolayı hizmetin Environment bölümünden alın. Elle Web Service kurduysanız en az 16 karakterlik güçlü bir parola tanımlayın.
6. HTTPS adresini açın. Tarayıcının giriş penceresinde kullanıcı adı **`gazi`**, parola **`APP_PASSWORD`** değeridir. Tarayıcılar bu oturumu bir süre saklayabilir; ortak bilgisayarda ayrı profil veya gizli pencere kullanın.

Bu depoyu başka bir deponun içinde `sunucu/` alt klasörüne koyarsanız barındırma hizmetinde Root Directory ayarını `sunucu` yapın. Önerilen kurulum, klasör içeriğinin doğrudan depo kökünde bulunmasıdır.

### Diğer Node.js sunucuları

Çalıştırma komutu `npm start` olur. `NODE_ENV=production`, `HOST=0.0.0.0`, `GEMINI_API_KEY`, `GEMINI_MODEL` ve en az 16 karakterlik `APP_PASSWORD` tanımlayın. `PORT` değerini barındırma hizmetiniz sağlayabilir. Uygulama dış ağa açılırken yeterli parola yoksa başlamaz. HTTPS'yi barındırma hizmeti veya ters vekil sağlamalıdır; parolayı düz HTTP üzerinden kullanmayın.

## Kullanım

Proje hazırlama → TEKNOFEST → Proje ve takım → Fikir ve ayrıntılar → Sunum metinleri yolunu izleyin. Proje adını ve en az 30 karakterlik açıklamasını girdikten sonra **Gemini ile sunum metni oluştur** düğmesini kullanın. Yanıt önce inceleme ekranında gösterilir; **Taslağı uygula** demeden mevcut metinler değişmez.

Gemini'ye yalnızca proje konusu, açıklaması ve teknik ayrıntılar gönderilir; takım üyelerinin adları, takım ID'si ve öğrenci kayıtları gönderilmez. Proje açıklamasına kendiniz yazdığınız bilgiler bu gönderime dahildir. Gemini internet araştırması yapmaz; eksik bilgiler `[Tamamlanmalı: …]` biçiminde belirtilir. Kaynakları ve iddiaları doğrulayın. API kullanım ücreti ve kota, kendi Google hesabınıza bağlıdır.

Takvim ve SWOT'u tamamlayıp Kontrol ve PDF adımından PDF'yi önizleyebilir veya indirebilirsiniz. TEKNOFEST sunumu yüklediğiniz **2025 Eğitim Teknolojileri** şablonuna dayanır; güncel yarışma şartnamesiyle ayrıca karşılaştırın. Bölümlerin 1/2 sayfalık sınırları, toplam 16 sayfa ve 75 MB sınırı kontrol edilir. TÜBİTAK alanında kaynak belgeler ve temel yazı taslağı bulunur; ayrıntılı TÜBİTAK PDF akışı bu sürüme dahil değildir.

Öğrenciler ve taslaklar **tarayıcının localStorage alanında** saklanır. Sunucu veritabanına kaydedilmez ve cihazlar arasında otomatik eşitlenmez. Tarayıcı verilerini temizlemeden veya başka adrese geçmeden önce taslak yedeğini indirin. `.json` yedeklerini GitHub'a koymayın.

## Testler ve hata giderme

```sh
npm run check
npm test
```

Testler gerçek API anahtarı kullanmadan sunucuyu, giriş kontrolünü, hatalı istekleri, Gemini yanıtlarının işlenmesini ve anahtarın tarayıcıya sızmamasını denetler. Canlı Gemini çağrısı için sizin anahtarınız, erişilebilir modeliniz ve kotanız gerekir; simülasyon testleri bunları doğrulamaz.

- Düğme kapalı: `.env` / hizmet değişkenlerindeki anahtarı kontrol edip sunucuyu yeniden başlatın.
- Erişim reddedildi: Google API anahtarınızın Gemini erişimini ve kısıtlamalarını kontrol edin.
- Model bulunamadı: `GEMINI_MODEL` değerini hesabınızın erişebildiği modele değiştirin.
- Kota doldu: Google kotasını ve faturalandırmayı kontrol edin; biraz sonra tekrar deneyin.
- PDF metni sığmıyor: Uyarıda belirtilen bölümü kısaltın. Metin kırpılarak sessizce kaybedilmez.

## Dosyalar ve kaynaklar

`public/assets/` altındaki kılavuz ve sunum şablonu, yüklediğiniz belgelerin dağıtım için küçültülmüş kopyalarıdır. Ana klasörünüzdeki özgün belgeler değiştirilmemiştir. PDF oluşturmak için kullanılan temiz sunum tabanı, yazı tipi ve tarayıcı kütüphaneleri de pakete dahildir.

Gemini bağlantısı resmî REST `generateContent` uç noktasını ve yapılandırılmış JSON çıktısını kullanır: https://ai.google.dev/api/generate-content

Üçüncü taraf kütüphane ve yazı tipi lisansları `THIRD_PARTY_NOTICES.md` dosyasında belirtilmiştir. Sizin yüklediğiniz belgelerin ve görsellerin kullanım hakları size aittir; depoyu herkese açık yaparken bunları dikkate alın.
