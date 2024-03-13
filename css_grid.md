# CSS Grid Notları

Grid CSS ile Layout'u dizayn etmek, Flexbox ile Layout içindeki parçaları dizayn etmek daha uygundur.

## CSS Grid Terminolojisi

`Grid Container`: Layout'u kapsayan bölge.
`Grid Cell`: Grid Container içindeki her bir bölüm.
`Grid Area`: Grid'in bir veya birden fazla `Grid Cell` içeren bölümü (kare veya diktörtgen bölge).
`Grid Item`: `Grid Container` içindeki `Grid Cell` veya `Grid Area` içine yerleşen her bir ana parça.
`Track`: Grid'in komple bir satırı veya sütunu.
`Grid Gap`: Grid Item'lar arsındaki boşluklar.

Grid Item diğer bir Grid Item üzerine overlap edebilir.
Nested (içiçe) grid layout oluşturulabilir. Yani bir grid item aynı zamanda bir <display: grid;> olabilir.

`explicit grid`: Grid satır ve sütunları kendimiz tanımlıyoruz.
`implicit grid`: Grid satır ve sütunları tanımlamıyoruz, grid kendisi dinamik olarak hallediyor.

## Grid - Flexbox Arasındaki Farklar

- Flexbox bir boyutludur, Grid ise iki boyutludur.

## Grid CSS'ye özel CSS komutları

```css
.grid_container{
  display: grid;

  grid-template-columns: 200px 100px;
  grid-template-columns: 2fr 1fr;
  grid-template-columns: 200px 2fr 1fr; // available space fr'lara göre dağıtılır.
  grid-template-columns: 200px auto 100px; /* auto kullanıldığında grid item'ın yerleşebileceği kadar yer açılır. Dolayısıyla auto satır genişliği bu sütuna denk gelen grid item'lardan en geniş olanına göre şekillenir.*/
  grid-template-columns: repeat(4, 100px);f
  grid-template-columns: auto repeat(4, 100px);
  grid-template-columns: fit-content(300px) repeat(4, 100px); /* fit-content: içeriği grid cell'e göre ayarlıyor, örneğin kelimeyi bir alta kaydırıyor, verilen genişli değerinin dışına çıkmıyor. Genişlik büyürse auto gibi davranıp bu sütun genişliği de büyüyor.*/
  grid-template-columns: repeat(4, 1fr 2fr); // every other item takes up twice
  grid-template-columns: repeat(4, 1fr auto);
  grid-template-columns: repeat(4, minmax(100px, auto));
  grid-template-columns: 2fr repeat(5, 1fr) 2fr;
  grid-auto-columns: 250px; //grid-auto-flow: column; ise yeni yarattığı sütunlar için bu dikkate alınır

  /* grid-line'lara isim de verilebilir. Hatta aynı grid line birden fazla isimle de isimlendirilebilir. */
  grid-template-columns: [site-left] 200px [content-left] 2fr [content-right] 1fr [site-right];
  grid-template-rows: [content-top] repeat(10, 1fr) [content-bottom];
  grid-template-columns: [sitebar-left] 200px [sitebar-right content-left] 2fr [content-right x-start] 1fr [x-end];

  /* implicitly, yani otomatik olarak media sorgusu yaparak ve çıkarımsal olarak column sayısını browserın belirlemesi için auto-fit veya auto-fill kullanabiliriz.
  auto-fit : browser genişliği büyükse ve item sayısı az ise sonda oluşan boşluğu itemlara dağıtır.
  auto-fill: sonda oluşan boşluğu itemlara dağıtmaz, sona görünmeyen columnlar ekler. */
  grid-template-columns: repeat(auto-fit, 300px);
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));


  grid-template-rows: 200px 150px; // birinci ve ikinci row tanımlanmış
  grid-template-rows: 60px 1fr 60px; // raw'da fr kullanılırsa explicit olarak height belirtmemiz gerekir ki ona göre dolmayan kısnı fr'a tahsis edebilsin.
  grid-auto-rows: 250px; //tanımlanmayan rowlar
  grid-auto-rows: 250px 400px; //tanımlanmayan rowlar için iki değer de girebiliriz
  grid-auto-rows: minmax(150px, auto); //minimum 150px olsun, ama içerik uzunsa uzasın.

  vaya tek satırda
  grid-template: 200px 150px / 2fr repeat(5, 1fr) 2fr; // önce raw sonra column templateler yazılabilir.

  /* Grid sisteminde yerleştirme default değeri raw'dur, yani önce bir satır tamamlanır sonra diğer satıra geçilir. column dersek grid item'ları önce sütun tamamlanarak yerleştirilir, yani satır sayısı dolmuşsa yeni column yaratarak yerleştirilir. dense ise grid itemların en az boşluk kalacak şekilde sırasını değiştirerek otomatik yerleştirilmesi için kullanılır. */
  grid-auto-flow: raw | column | dense; //

  grid-row-gap: 20px;
  grid-column-gap: 10px;
  grid-gap: 20px 10px; // önce raw sonra columnlar arası boşluklar
  grid-gap: 15px; // hem row hem de columnlar arasında boşluk bırakır.

  grid-template-areas: // bir cell boş kalacaksa template içinde ilgili yere nokta . konulabilir
    "header header header"
    "sidebar content content"
    "sidebar . links"
  /* area isimleri birer   emoji bile olanilir. */

  /* hepsini birarada ayarlayalım */
  grid-template: // her bir satırın yüksekliği / adından column yapısı
    "header header header" 60px
    "sidebar content content" 1fr
    "sidebar . links" 60px
    / %20 3fr 1fr

  /* @ justify- works in row axis - bir satır içinde / satır boyunca yerleştirme yapar
     @ align- works in column axis - bir sütun içinde / sütun boyunca yerleştirme yapar

     @ align vermek için bir yüksekliğin belirli olması gerekmektedir

     @ -content ayarında grid item'lar bir bütün olarak değerlendirilir ve grid yapısı viewport/container içinde belirtilen şekilde yerleştirilir. Grid yapısı kendisini barındıran container'dan bir şekilde küçük ise bu işe yarar, aksi takdirde fraction'larla örneğin zaten tüm alan kullanılıyorsa bu yerleştirmenin bir anlamı kalmaz, gerek yoktur.
     @ -items ayarında her bir grid item'ın grid cell içinde belirli bir düzene göre yerleştirilmesi söz konusudur.
  */
  https://css-tricks.com/snippets/css/complete-guide-grid/
  https://cssgrid.io

  justify-content: *start* | end | center | stretch | space-around | space-between | space-evenly;
  align-content: *start* | end | center | stretch | space-around | space-between | space-evenly;

  place-content: center / end ; // <align-content> / <justify-content>
  place-content: center; // both <align-content> and <justify-content> are center

  justify-items: start | end | center | *stretch*;
  align-items: start | end | center | *stretch*;

  place-items: center end ; // sırasıyla <align-items> ve <justify-items> değerleri
  place-items: center; // both <align-items> and <justify-items> are center


  justify-content: center;
  align-content: center;
  height: 100vh; // vertical height %100

  justify-items: center; // default scretch, main axiste yerleşmeyi düzenliyor.
  align-items: center; // cross axiste yerleşmeyi düzenliyor.

  place-items: center;
}

.grid_item_header{
  grid-area: header;

  veya

  grid-column-start: 1; // 1nci grid çizgisinden başla
  grid-column-end: 3; //  3'ncü grid çizgisinde bitir
  grid-column-start: 1;
  grid-column-end: -1; // son satır çizisi demek
  /* start ve end parametrelerinden sadece birisini de kullanabiliriz, bu takdirde belirtilmeyen değeri dikkate almadan start veya end noktası dikkate alınarak yerleştirme yapılır. */
  grid-column: 1 / -1; // baştan sona kadar kapsar
  grid-column: 1 / -2; // baştan başlayarak sondan bir önceki grid çizgisine kadar kapsar
  grid-column: 1 / 3; // yatayda 1nci/ilk grid çizgisi ile 3'ncü grid çizgisi arası, yani ilk iki sütun
  grid-column: span 3; // nerdeyse ordan başla üç column kapsa, fakat burada kapsayabileceği üç sütun kadar yer yok ise buraları *boş bırakır*, bir alt satıra geçerek üç yer kaplar. İşte burada dense parametresi devreye girebilir.
  grid-column: span 10; // yaratılan sütun sayısından fazla bir yer kaplanması belirtildiğinde implicitly olarak browser yeni column'lar yaratır ve bu item'ı yerleştirir.
  grid-column: span 2 / 5; // 5'nci sütun çizgisinde bitecek şekilde iki bölüm kapsar.
  grid-column: 2 / span 2; // 2'nci sütun çizgisinden başlayarak iki bölüm kapsar.

  /* grid-line'lara isim verilmiş ise grid item'ları bunları refere ederek de yerleştirebiliriz. */
  grid-column: content-left /  content-right;
  grid-column: site-left /  span 2;
  grid-row: content-top /  span 2;
  grid-row-end: content-bottom;

  /* Grid area tanımlanmış ise, bir bir item'ı bu grid area'ların baladığı bittiği yerleri refere ederek de yerleştirebiliriz. */
  grid-column: area1-start / area1-end;
  grid-column: area1-start / area2-end;

  grid-row-start: 1;
  grid-row-end: 4;
  grid-row: 2 / 4; // düşeyde 2nci grid çizgisi ile 4'ncü grid çizgisi arası
  grid-row: 2 / span 2; // ikinci grid çizgisinden başla iki bölüm kapsa
  grid-row: span 2; // nerdeyse ordan başla iki raw kapsa

  veya
  grid-area: 1 / 1 / 2 / 4; // raw-start / column-start / raw-end / column-end
  grid-area: 1 / 1 / span 1 / span 3; // raw-start / column-start / raw sayısı / column sayısı

  z-index: 1; // overlap eden grid cell için göreceli üste olması ayarlanabilir


  /* start | end | center | stretch */
  align-self: start; // grid cell içinde vertical dikey yerleştirme
  justify-self: center; // horizantal yatay yerleştirme

  place-self: start center;  // <align-self> <justify-self> değerleri
  place-self: center; // her ikisi de
}

.grid_item_sidebar{
  grid-area: sidebar;

  veya
  order: -1; // default 0'dır, dolayısıyla bu item en başa geçer
  order: 1; // default 0'dır, diğerleri 0 olduğunda dolayısıyla bu item en son sıraya geçer
  /* order ile çok oynamamak lazım, çünkü screen reader'lar html üzerinden okuyor. */
}

.grid_item_content{
  grid-area: content;
}
```

Nested grid ile yapılmış resposive bir grid yapısı örneği;

```html
<body>
  <div class="albums">
    <div class="album">
      <img
        src="https://source.unsplash.com/random/300x300?v=1"
        class="album__artwork"
      />
      <div class="album__details">
        <h2>Album Title</h2>
        <p class="album__artist">Artist Name</p>
        <p class="album_desc">
          Lorem, ipsum dolor sit amet consectetur adipisicing elit. Nemo
          voluptas odit blanditiis enim ducimus quo molestiae explicabo officiis
          possimus laboriosam.
        </p>
      </div>
    </div>
  </div>
</body>
```

```css
<style>
  .albums {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); /* responsiveness */
    grid-gap: 20px;
  }

  .album {
    background: rgba(255, 255, 255, 0.2);
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
    padding: 20px;
    color: white;
    font-weight: 100;
    display: grid; /* nested */
    grid-template-columns: 150px 1fr;
    align-items: center;
  }

  .album__artwork {
    width: %100; /* bunu belirtmez isek değişik davranıyor */
  }
</style>
```
