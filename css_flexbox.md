# CSS Flexbox Notları

Flexbox ile Layout içindeki parçaları dizayn etmek daha uygundur.

## CSS Flexbox Terminolojisi

Layout'u kapsayan bölge ``Grid Container`` olarak isimlendirilmektedir.
Grid Container içindeki her bir parça ``Grid Item`` olarak isimlendirilmektedir.
Grid Item'lar arsındaki boşluklar ``Gap`` olarak isimlendirilmektedir.


## Grid Flexbox'a özel CSS komutları


```css
.flex_container{
  display: flex;
  display: inline-flex;

  flex-direction: row | column | row-reverse | column-reverse; 
  /* defult değer raw'dur. Raw ise item'lar yatay yerleşiyor, main axis yatay, cross axis dikey oluyor.  Column ise item'lar dikey yerleşiyor, main axis dikey, cross axis yatay oluyor. */
  
  flex-wrap: wrap | nowrap | wrap-reverse; 
  /* wrap ise ekrana yani viewport'a sığmayan item bir diğer satır veya sütuna (flex-direction baz alınarak) geçer, nowrap ise sığmayan item view dışına görünmez şekilde taşar. */

  flex-flow: column wrap; 
  flex-flow: row nowrap;
  /* flex-direction ve flex-wrap parametreleri tek bir satırda belirtilebilir. */

  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
  align-items: flex-start; flex-end; center; space-between; space-around; space-evenly;

  align-items: baseline; // itemları içindeki bilgiye göre hizalar
  
  align-content: flex-start; flex-end; center; space-between; space-around; space-evenly;
  height: 700px; // align-content için spesific bir yükseklik girilmesi gerekiyor.
  /* 
  justify-content ----> main axiste yerleşmeyi düzenliyor.
  align-items --------> cross axiste itemların birbirine göre hizasını düzenliyor.
  align-content ------> cross axiste itemların bir grup olarak yerleşmesini düzenliyor.  
  */

  .flex-container > * {
    margin: 10px;
    flex: 1;
  } /* flex item'ların her birine eşit flex verildiğinde flex-container'a fit yani stretch olurlar */
}

.flex_item{
  width: 200px;
  margin: 10px;
  border: 3px solid #333;
  background-color: #dfdfdf;

  /* item içeriğinin center yapılması için */
  display: flex;
  justify-content: center;
  align-items: center;
}

.flex_item_1{
  min-height: 100px;

  flex-shrink: 0; // view küçülürken küçülmemesi sağlanır, aksi takdirde orantısal daralır.
  flex-grow: 1; // diğerleri 0 ise boş yeri bu item kaplar
  /* shrink ve grow değerleri width değeri baz alınarak (direction column ise height değer
  i) daralma ve genişlemede daralan veya genişleyen kadar alanın hangi item'a hangi oranda pay edileceğini belirlememize yarar.*/

  order: 2; // her bir itema sıra no verilerek gösterim sırası değiştirilebilir.

  veya kısaca
  flex: 1 0 0px; // sırasıyla flex-grow flex-shrink flex-basis parametreleri
  flex: 5 5 %25; 
  flex: 1 0 auto;
  flex: 1 1 300px;
}

.flex_item_2{
  min-height: 200px;
  flex-grow: 2; // açıkta kalan alana diğer bire göre ikilik oranda yayılır.
  flex-basis: 0; %15; // bu ve diğerinde kullanılırsa, grow iki olan bire göre tam iki kat olur

  align-self: center; // sadece bu item vertically center olur.

.flex_item_3{
  min-height: 300px;  
  flex-grow: 1; // açıkta kalan alana birlik oranda yayılır.
  flex-basis: 0; 
}
```