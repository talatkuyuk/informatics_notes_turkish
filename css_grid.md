# CSS Grid Notları

Grid CSS ile Layout'u dizayn etmek, Flexbox ile Layout içindeki parçaları dizayn etmek uygundur.

## CSS Grid Terminolojisi

Layout'u kapsayan bölgeye ``Grid Container`` olarak isimlendirilmektedir.
Grid Container içindeki her bir parça ``Grid Item`` olarak isimlendirilmektedir.
Grid Item'lar arsındaki boşluklar ``Gap`` olarak isimlendirilmektedir.

## Grid - Flexbox Arasındaki Farklar

+ Flexbox bir boyutludur, Grid ise iki boyutludur.

## Grid CSS'ye özel CSS komutları


```css
.classname {
  display: grid;
  grid-template-columns: 200px 100px;
  grid-template-columns: 2fr 1fr;
  grid-template-columns: repeat(4, 100px);
  grid-template-columns: 2fr repeat(5, 1fr) 2fr;
  grid-template-rows: 200px 150px; // birinci ve ikinci row tanımlanmış
  grid-auto-rows: 250px; //tanımlanmayan rowlar
  grid-auto-rows: minmax(150px, auto); //minimum 150px olsun, ama içerik uzunsa uzasın.
  grid-row-gap: 20px;
  grid-column-gap: 10px;
  grid-gap: 15px; // hem row hem de columnlar arasında boşluk bırakır.

}
```

## HTML için TAB yapılarak girilen kısaltmalar
!
lorem50
div
