script.js kodlarının açıklaması:

Bu kod, `MomentumSlider` adlı bir slider kütüphanesini kullanarak dört farklı slider (sürgü) oluşturur. Sliderlar, belirli içerikleri senkronize bir şekilde gösterir ve kullanıcı etkileşimleriyle (örneğin, tıklama) kontrol edilebilir. Aşağıda kodun detaylı açıklaması bulunmaktadır:

### Genel Yapı ve Değişkenler

```javascript
(function() {

    var slidersContainer = document.querySelector('.sliders-container');
```
- **Anonim Fonksiyon**: Kod bir anonim fonksiyon içine alınarak, global scope kirlenmesi önlenir.
- **`slidersContainer`**: HTML'deki `.sliders-container` sınıfına sahip elementi seçer ve bu elemana sliderlar eklenir.

### Numbers Slider (Sayılar Slider'ı)

```javascript
    var msNumbers = new MomentumSlider({
        el: slidersContainer,
        cssClass: 'ms--numbers',
        range: [1, 4],
        rangeContent: function (i) {
            return '0' + i;
        },
        style: {
            transform: [{scale: [0.4, 1]}],
            opacity: [0, 1]
        },
        interactive: false
    });
```
- **`el`**: Sliderın ekleneceği element.
- **`cssClass`**: Slidera uygulanacak CSS sınıfı.
- **`range`**: Sliderın içerik aralığı. Burada 1'den 4'e kadar.
- **`rangeContent`**: İçerik oluşturma fonksiyonu. Her sayı için '0' ile başlayan bir sayı döndürür.
- **`style`**: Sliderın stili. Ölçek ve opaklık arasında geçiş yapar.
- **`interactive`**: Etkileşimli olmadığını belirtir.

### Titles Slider (Başlıklar Slider'ı)

```javascript
    var titles = [
        'Steven Paul Jobs',
        'Thomas Preston-Werner',
        'Bill Gates',
        'Elon Musk'
    ];
    var msTitles = new MomentumSlider({
        el: slidersContainer,
        cssClass: 'ms--titles',
        range: [0, 3],
        rangeContent: function (i) {
            return '<h3>'+ titles[i] +'</h3>';
        },
        vertical: true,
        reverse: true,
        style: {
            opacity: [0, 1]
        },
        interactive: false
    });
```
- **`titles`**: Başlıkların listesi.
- **`rangeContent`**: Başlıkları oluşturur ve `<h3>` etiketleri içinde döner.
- **`vertical`**: Sliderın dikey olduğunu belirtir.
- **`reverse`**: Sliderın ters çalışmasını sağlar.
- **`style`**: Opaklık stilini ayarlar.

### Links Slider (Linkler Slider'ı)

```javascript
    var msLinks = new MomentumSlider({
        el: slidersContainer,
        cssClass: 'ms--links',
        range: [0, 3],
        rangeContent: function () {
            return '<a class="ms-slide__link"></a>';
        },
        vertical: true,
        interactive: false
    });
```
- **`rangeContent`**: Boş linkler oluşturur (`<a>` etiketi).

### Pagination (Sayfalandırma)

```javascript
    var pagination = document.querySelector('.pagination');
    var paginationItems = [].slice.call(pagination.children);
```
- **`pagination`**: HTML'deki `.pagination` sınıfına sahip elementi seçer.
- **`paginationItems`**: Sayfalandırma elemanlarını bir diziye çevirir.

### Images Slider (Görseller Slider'ı)

```javascript
    var msImages = new MomentumSlider({
        el: slidersContainer,
        cssClass: 'ms--images',
        range: [0, 3],
        rangeContent: function () {
            return '<div class="ms-slide__image-container"><div class="ms-slide__image"></div></div>';
        },
        sync: [msNumbers, msTitles, msLinks],
        style: {
            '.ms-slide__image': {
                transform: [{scale: [1.5, 1]}]
            }
        },
        change: function(newIndex, oldIndex) {
            if (typeof oldIndex !== 'undefined') {
                paginationItems[oldIndex].classList.remove('pagination__item--active');
            }
            paginationItems[newIndex].classList.add('pagination__item--active');
        }
    });
```
- **`rangeContent`**: Görsel konteynerlerini ve içindeki görselleri oluşturur.
- **`sync`**: Diğer sliderlar ile senkronize olur.
- **`style`**: Görsellerin ölçeğini ayarlar.
- **`change`**: Slider değiştiğinde, sayfalandırma elemanlarının aktifliğini günceller.

### Pagination Click Event (Sayfalandırma Tıklama Olayı)

```javascript
    pagination.addEventListener('click', function(e) {
        if (e.target.matches('.pagination__button')) {
            var index = paginationItems.indexOf(e.target.parentNode);
            msImages.select(index);
        }
    });

})();
```
- **`addEventListener`**: Sayfalandırma butonlarına tıklama olayını dinler.
- **`matches`**: Tıklanan elemanın `.pagination__button` sınıfına sahip olup olmadığını kontrol eder.
- **`indexOf`**: Tıklanan elemanın dizideki indexini bulur.
- **`select`**: İlgili slider öğesini seçer.

### Özet
Bu kod, dört farklı sliderı oluşturur ve bunları senkronize eder. Kullanıcı sayfalandırma butonlarına tıkladığında, tüm sliderlar senkronize bir şekilde değişir. `MomentumSlider` kütüphanesi ile kolayca dinamik ve etkileyici sliderlar oluşturulabilir.

index.html kodlarının açıklaması:

Bu HTML belgesi, bir web portföyü için senkronize sliderları içeren bir yapı oluşturur. 
Belge, normalize.css kullanarak tarayıcı tutarlılığını sağlar ve MomentumSlider kütüphanesi ile etkileşimli ve senkronize sliderları oluşturur. Aşağıda kodun detaylı açıklaması bulunmaktadır:

### HTML Belgesinin Yapısı

#### `<!DOCTYPE html>`
HTML5 belgesinin türünü belirtir.

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Portfolio with Synchronized Slider</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/5.0.0/normalize.min.css">
  <link rel="stylesheet" href="./style.css">
</head>
<body>
```
- **`<html lang="en">`**: Belgenin dilini İngilizce olarak ayarlar.
- **`<meta charset="UTF-8">`**: Belgenin karakter setini UTF-8 olarak ayarlar.
- **`<title>`**: Belgenin başlığını belirler.
- **`<link rel="stylesheet" href="...">`**: normalize.css ve yerel style.css dosyasını dahil eder.

### Ana Yapı

```html
<div class="container">
    <header class="header">
        <a class="header__logo"><i>OPERATION EAGLE</i></a>
        <nav class="header__menu">
            <ul class="header__menu__list">
                <li class="header__menu__item"><a class="header__menu__link"><i><strong>Skills</strong></i></a></li>
                <li class="header__menu__item"><a class="header__menu__link"><i><strong>Works</strong></i></a></li>
                <li class="header__menu__item"><a class="header__menu__link"><i><strong>My Documents</strong></i></a></li>
                <li class="header__menu__item"><a class="header__menu__link"><i><strong>About Me</strong></i></a></li>
                <li class="header__menu__item"><a class="header__menu__link"><i><strong>Contact</strong></i></a></li>
            </ul>
        </nav>
    </header>
```
- **`<div class="container">`**: Ana kapsayıcı div.
- **`<header class="header">`**: Başlık bölümünü tanımlar.
- **`<a class="header__logo"><i>OPERATION EAGLE</i></a>`**: Başlık logosunu içerir.
- **`<nav class="header__menu">`**: Menü navigasyonunu içerir.
- **`<ul class="header__menu__list">`**: Menü öğelerini listeleyen bir liste.

### Slider ve Sayfalandırma

```html
    <main class="sliders-container">
        <!-- Here will be injected sliders for images, numbers, titles and links -->
        <!-- Simple pagination for the slider -->
        <ul class="pagination">
            <li class="pagination__item"><a class="pagination__button"></a></li>
            <li class="pagination__item"><a class="pagination__button"></a></li>
            <li class="pagination__item"><a class="pagination__button"></a></li>
            <li class="pagination__item"><a class="pagination__button"></a></li>
        </ul>
    </main>
```
- **`<main class="sliders-container">`**: Sliderlar için ana kapsayıcı.
- **`<ul class="pagination">`**: Sayfalandırma butonlarını içeren liste.
- **`<li class="pagination__item"><a class="pagination__button"></a></li>`**: Her sayfalandırma butonu için bir liste öğesi ve buton.

### Alt Bilgi (Footer)

```html
    <footer class="footer">
        <nav class="footer__menu">
            <ul class="footer__menu__list">
                <li class="footer__menu__item"><a class="footer__menu__link"><i><strong>Twitter</strong></i></a></li>
                <li class="footer__menu__item"><a class="footer__menu__link"><i><strong>Linkedin</strong></i></a></li>
                <li class="footer__menu__item"><a class="footer__menu__link"><i><strong>Instagram</strong></i></a></li>
            </ul>
        </nav>
    </footer>
</div>
```
- **`<footer class="footer">`**: Alt bilgi bölümünü tanımlar.
- **`<nav class="footer__menu">`**: Alt bilgi navigasyon menüsünü içerir.
- **`<ul class="footer__menu__list">`**: Alt bilgi menü öğelerini listeleyen bir liste.

### Javascript Kütüphaneleri ve Dosyalar

```html
<!-- partial -->
<script src='https://rawgit.com/lmgonzalves/momentum-slider/master/dist/momentum-slider.min.js'></script>
<script src="./script.js"></script>
</body>
</html>
```
- **`<script src='...momentum-slider.min.js'></script>`**: MomentumSlider kütüphanesini dahil eder.
- **`<script src="./script.js"></script>`**: Yerel script.js dosyasını dahil eder.

### Özet

Bu HTML belgesi, normalize.css ile tarayıcı tutarlılığını sağlar ve MomentumSlider kütüphanesini kullanarak senkronize sliderları oluşturur. 
Başlık, menü, sliderlar ve alt bilgi bölümleri belirli sınıflar ile stilize edilir ve script.js dosyasında sliderların işlevselliği sağlanır. 
Sliderlar, kullanıcı etkileşimleriyle (örneğin, sayfalandırma butonlarına tıklama) senkronize bir şekilde kontrol edilir.

style.css kodlarının açıklaması:

Bu CSS dosyası, HTML belgesinde bulunan farklı bileşenler için çeşitli stil kurallarını içerir. Aşağıda, her stil kuralının detaylı açıklaması bulunmaktadır:

### Genel Stil Kuralları

```css
*, *:before, *:after {
  box-sizing: border-box;
}

body {
  color: white;
  background-color: #1B1C21;
  overflow: hidden;
}

a {
  color: white;
  text-decoration: none;
  cursor: pointer;
}
```
- **`*, *:before, *:after`**: Tüm öğeler ve pseudo öğeler için box-sizing özelliğini `border-box` olarak ayarlar.
- **`body`**: Beyaz metin rengi, koyu arka plan rengi ve gizli taşma ayarları yapar.
- **`a`**: Tüm bağlantılar için beyaz renk, alt çizgi olmaması ve imleç değişimi ayarları yapar.

### Ana Kapsayıcı ve Katmanlar

```css
.container {
  position: relative;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: rgba(0, 0, 0, 0.1);
}
.container:before {
  content: "";
  position: absolute;
  left: -150%;
  top: 0;
  width: 300%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.3);
  transform: rotate(45deg);
  z-index: -1;
}
```
- **`.container`**: Esnek kutu modeli kullanarak dikey yönlü düzen ve minimum yüksekliği tam ekran olarak ayarlar.
- **`.container:before`**: Arka plan efektleri için döndürülen büyük bir dikdörtgen oluşturur.

### Başlık (Header)

```css
.header {
  display: flex;
  align-items: center;
  padding: 30px;
}

.header__logo {
  font-size: 1.3em;
  font-weight: 900;
  letter-spacing: -1px;
}
.header__logo span {
  display: inline-block;
  transform: translateY(4px) rotate(180deg);
  pointer-events: none;
}

.header__menu {
  margin-left: auto;
}

.header__menu__list, .footer__menu__list {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.header__menu__link {
  margin-left: 50px;
}
```
- **`.header`**: Başlık bölümünü esnek kutu modeli ile yatay hizalar ve 30px iç boşluk ekler.
- **`.header__logo`**: Logonun yazı tipi boyutunu ve ağırlığını ayarlar, harfler arası boşluğu azaltır.
- **`.header__logo span`**: Logodaki harfin döndürülmesi ve dikey hizalanması.
- **`.header__menu`**: Menü öğelerini sağa hizalar.
- **`.header__menu__list`**, **`.footer__menu__list`**: Menü listelerinin esnek düzenlemesi ve varsayılan stil kaldırılması.
- **`.header__menu__link`**: Menü bağlantıları arasına 50px boşluk ekler.

### Alt Bilgi (Footer)

```css
.footer {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 30px;
}

.footer__menu__link {
  margin-left: 50px;
  color: rgba(255, 255, 255, 0.5);
}
```
- **`.footer`**: Alt bilgi bölümünü esnek kutu modeli ile yatay hizalar, sağa hizalar ve 30px iç boşluk ekler.
- **`.footer__menu__link`**: Alt bilgi bağlantıları arasına 50px boşluk ekler ve renklerini yarı saydam yapar.

### Slider Kapsayıcı (Sliders Container)

```css
.sliders-container {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex: 1;
}
```
- **`.sliders-container`**: Sliderlar için merkezi hizalama sağlar ve esnek büyüme özelliği ekler.

### Görüntü Sliderı (Image Slider)

```css
.ms--images {
  position: relative;
  overflow: hidden;
}
.ms--images.ms-container--horizontal {
  width: 100%;
  height: 400px;
  max-width: 100%;
}
.ms--images.ms-container--horizontal .ms-track {
  left: calc(50% - 350px);
}
.ms--images.ms-container--horizontal .ms-slide {
  display: inline-flex;
}
.ms--images .ms-track {
  display: flex;
  position: absolute;
  white-space: nowrap;
  padding: 0;
  margin: 0;
  list-style: none;
}
.ms--images .ms-slide {
  align-items: center;
  justify-content: center;
  width: 700px;
  height: 400px;
  -webkit-user-select: none;
     -moz-user-select: none;
      -ms-user-select: none;
          user-select: none;
}

.ms--images {
  left: calc(50% - 280px);
}
.ms--images.ms-container--horizontal .ms-track {
  left: -70px;
}
.ms--images .ms-slide:nth-child(1) .ms-slide__image {
  background-image: url("Apple\ Computer.jpg");
}
.ms--images .ms-slide:nth-child(2) .ms-slide__image {
  background-image: url("Github.jpg");
}
.ms--images .ms-slide:nth-child(3) .ms-slide__image {
  background-image: url("Microsoft.jpg");
}
.ms--images .ms-slide:nth-child(4) .ms-slide__image {
  background-image: url("spacex.jpg");
}
.ms--images .ms-slide__image-container {
  width: 80%;
  height: 80%;
  background-color: rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
.ms--images .ms-slide__image {
  width: 100%;
  height: 100%;
  background-size: cover;
}
```
- **`.ms--images`**: Görüntü sliderının temel ayarları.
- **`.ms--images.ms-container--horizontal`**: Yatay düzen ayarları.
- **`.ms--images .ms-track`**: Slider parçasının konum ve düzen ayarları.
- **`.ms--images .ms-slide`**: Slider öğelerinin boyut ve hizalama ayarları.
- **`.ms--images .ms-slide:nth-child(1) .ms-slide__image`**: Her bir slayt için farklı arka plan resimleri ayarları.
- **`.ms--images .ms-slide__image-container`**: Görüntü kapsayıcısının boyut ve arka plan ayarları.
- **`.ms--images .ms-slide__image`**: Görüntülerin boyut ve kaplama ayarları.

### Numara Sliderı (Number Slider)

```css
.ms--numbers {
  position: relative;
  overflow: hidden;
}
.ms--numbers.ms-container--horizontal {
  width: 240px;
  height: 240px;
  max-width: 100%;
}
.ms--numbers.ms-container--horizontal .ms-track {
  left: calc(50% - 120px);
}
.ms--numbers.ms-container--horizontal .ms-slide {
  display: inline-flex;
}
.ms--numbers .ms-track {
  display: flex;
  position: absolute;
  white-space: nowrap;
  padding: 0;
  margin: 0;
  list-style: none;
}
.ms--numbers .ms-slide {
  align-items: center;
  justify-content: center;
  width: 240px;
  height: 240px;
  -webkit-user-select: none;
     -moz-user-select: none;
      -ms-user-select: none;
          user-select: none;
}

.ms--numbers {
  position: absolute;
  left: calc(50% - 380px);
  top: calc(50% - 300px);
  z-index: -1;
  pointer-events: none;
}
.ms--numbers .ms-slide {
  font-size: 9em;
  font-weight: 900;
  color: rgba(255, 255, 255, 0.2);
}
```
- **`.ms--numbers`**: Numara sliderının temel ayarları.
- **`.ms--numbers.ms-container--horizontal`**: Yatay düzen ayarları.
- **`.ms--numbers .ms-track`**: Slider parçasının konum ve düzen ayarları.
- **`.ms--numbers .ms-slide`**: Slider öğelerinin boyut, hizalama ve kullanıcı seçimi ayarları.
- **`.ms--numbers`**: Sliderın mutlak konumu ve z-index ayarları.
- **`.ms--numbers .ms-slide`**: Numara slaytlarının font boyutu, ağırlığı ve renk ayarları.

### Başlık Sliderı (Title Slider)

```css
.ms--titles {
  position: relative;
  overflow: hidden;
}
.ms--titles.ms-container--vertical {
 

 width: 400px;
  height: 170px;
  max-height: 100%;
}
.ms--titles.ms-container--vertical .ms-track {
  flex-direction: column;
  top: calc(50% - 85px);
}
.ms--titles.ms-container--vertical.ms-container--reverse .ms-track {
  flex-direction: column-reverse;
  top: auto;
  bottom: calc(50% - 85px);
}
.ms--titles.ms-container--vertical .ms-slide {
  display: flex;
}
.ms--titles .ms-track {
  display: flex;
  position: absolute;
  white-space: nowrap;
  padding: 0;
  margin: 0;
  list-style: none;
}
.ms--titles .ms-slide {
  align-items: center;
  justify-content: center;
  width: 400px;
  height: 170px;
  -webkit-user-select: none;
     -moz-user-select: none;
      -ms-user-select: none;
          user-select: none;
}

.ms--titles {
  position: absolute;
  left: calc(50% - 420px);
  top: calc(50% - 85px);
  z-index: 1;
  pointer-events: none;
}
.ms--titles .ms-track {
  white-space: normal;
}
.ms--titles .ms-slide {
  font-size: 3.3em;
  font-weight: 600;
}
.ms--titles .ms-slide h3 {
  margin: 0;
  text-shadow: 1px 1px 2px black;
}
```
- **`.ms--titles`**: Başlık sliderının temel ayarları.
- **`.ms--titles.ms-container--vertical`**: Dikey düzen ayarları.
- **`.ms--titles.ms-container--vertical.ms-container--reverse`**: Ters dikey düzen ayarları.
- **`.ms--titles .ms-track`**: Slider parçasının konum ve düzen ayarları.
- **`.ms--titles .ms-slide`**: Slider öğelerinin boyut ve hizalama ayarları.
- **`.ms--titles`**: Sliderın mutlak konumu ve z-index ayarları.
- **`.ms--titles .ms-slide`**: Başlık slaytlarının font boyutu ve ağırlığı ayarları.
- **`.ms--titles .ms-slide h3`**: Başlık metinlerinin kenar boşlukları ve gölge efekti.

### Bağlantı Sliderı (Link Slider)

```css
.ms--links {
  position: relative;
  overflow: hidden;
}
.ms--links.ms-container--vertical {
  width: 120px;
  height: 60px;
  max-height: 100%;
}
.ms--links.ms-container--vertical .ms-track {
  flex-direction: column;
  top: calc(50% - 30px);
}
.ms--links.ms-container--vertical .ms-slide {
  display: flex;
}
.ms--links .ms-track {
  display: flex;
  position: absolute;
  white-space: nowrap;
  padding: 0;
  margin: 0;
  list-style: none;
}
.ms--links .ms-slide {
  align-items: center;
  justify-content: center;
  width: 120px;
  height: 60px;
  -webkit-user-select: none;
     -moz-user-select: none;
      -ms-user-select: none;
          user-select: none;
}

.ms--links {
  position: absolute;
  left: calc(50% - 420px);
  top: calc(50% + 105px);
  z-index: 1;
}
.ms--links .ms-track {
  white-space: normal;
}
.ms--links .ms-slide__link {
  font-weight: 600;
  padding: 5px 0 8px;
  border-bottom: 2px solid white;
  cursor: pointer;
}
```
- **`.ms--links`**: Bağlantı sliderının temel ayarları.
- **`.ms--links.ms-container--vertical`**: Dikey düzen ayarları.
- **`.ms--links .ms-track`**: Slider parçasının konum ve düzen ayarları.
- **`.ms--links .ms-slide`**: Slider öğelerinin boyut ve hizalama ayarları.
- **`.ms--links`**: Sliderın mutlak konumu ve z-index ayarları.
- **`.ms--links .ms-slide__link`**: Bağlantı öğelerinin font ağırlığı, kenar boşlukları ve alt çizgi ayarları.

### Sayfalama (Pagination)

```css
.pagination {
  display: flex;
  position: absolute;
  left: calc(50% - 420px);
  top: calc(100%);
  list-style: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  z-index: 1;
}
.pagination__button {
  display: inline-block;
  position: relative;
  width: 36px;
  height: 20px;
  margin: 0 5px;
  cursor: pointer;
}
.pagination__button:before, .pagination__button:after {
  content: "";
  position: absolute;
  left: 0;
  top: calc(50% - 1px);
  width: 100%;
  box-shadow: 0 1px 0 #0B0D14;
}
.pagination__button:before {
  height: 2px;
  background-color: #6A3836;
}
.pagination__button:after {
  height: 3px;
  background-color: #DC4540;
  opacity: 0;
  transition: 0.5s opacity;
}

.pagination__item--active .pagination__button:after {
  opacity: 1;
}
```
- **`.pagination`**: Sayfalama öğelerinin yatay hizalanması ve konumlandırılması.
- **`.pagination__button`**: Sayfalama düğmeleri için boyut ve hizalama ayarları.
- **`.pagination__button:before`**: Düğmelerin altındaki ince çizgi.
- **`.pagination__button:after`**: Aktif düğme için daha kalın çizgi.
- **`.pagination__item--active .pagination__button:after`**: Aktif düğmenin belirginleştirilmesi.

### Medya Sorguları (Responsive Design)

```css
@media screen and (max-width: 860px) {
  .ms--numbers {
    left: calc(50% - 120px);
  }

  .ms--titles {
    left: calc(50% - 200px);
    top: calc(50% - 135px);
    text-align: center;
  }

  .ms--links {
    left: calc(50% - 60px);
    top: calc(50% + 80px);
  }

  .pagination {
    left: 50%;
    top: calc(100% - 50px);
    transform: translateX(-50%);
  }
}
@media screen and (max-width: 600px) {
  .ms--images {
    overflow: visible;
  }
}
@media screen and (max-width: 400px) {
  .ms--titles .ms-slide {
    transform: scale(0.8);
  }
}
```
- **`@media screen and (max-width: 860px)`**: 860px genişliğin altındaki ekranlar için stil ayarları.
- **`@media screen and (max-width: 600px)`**: 600px genişliğin altındaki ekranlar için stil ayarları.
- **`@media screen and (max-width: 400px)`**: 400px genişliğin altındaki ekranlar için stil ayarları.

Bu CSS kodları, responsive (duyarlı) tasarımı göz önünde bulundurarak çeşitli ekran boyutları için düzenlemeler sağlar. Farklı bileşenlerin düzenini ve görünümünü optimize eder.
