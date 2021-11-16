# CSS Notları

<input disabled required type="text | checkbox | button | radio | password">
<button tooltip="Tooltip">Submit</button>

```css



div {
    position: static | relative | absolute | fixed | sticky;
    display: block | inline | inline-block | flex | grid;
}

* {
    margin: 0;
    padding: 20px;
    box-sizing: border-box;
    font-weight: bold;
    font-size: 30px;
    font-family: 'Nunito';
}


[tooltip] {
    position: relative;
}
[tooltip]:hover::after {
    content: attr(tooltip);
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    margin-top: 5px;
    padding: 5px;
    background-color: #fff;
}

.className > div {
    background: #eee;
    width: %15;
    background-color: #fff;
    color: #aaa;
    min-height: 50px;
    /* 
    comment
    */
}

/* tek sıradaki divler, odd | even */
.className > div:nth-child(odd) {  
    background: #eee;
}

/* üçüncü li */
.li:nth-child(3) {   
    background: #eee;
}

.className {
    height: 100vh;
    border: 10px solid #cfcfcf;
    border-radius: 3px;
    background-color: #ccc;
    padding: 0.2em;
    text-transform: uppercase;
}

p {
    width: 200px;
    background: linear-gradient(to right, #renk1, #renk2);
}

@media(min-width: 760px){

}

@media(max-width: 760px){

}

img {
    display: block;
    width: 100%;
    box-shadow: -1px 0px 0px rgba(0, 0, 0, 0.06)
}

p {
    margin-top: 0;
    margin-left: 15px;
}


span {
    position: relative | absolute;
}

span:before {
    content: '';
    position: absolute;
    height: 1px;
    width: 10px;
    border-bottom: 1px solid black;
    top: 10px;
    left: -15px;
}


```
units

100px; sayfanın büyüklüğüne göre değişmeyen tam olarak 100px
50%; evebeyne tahsis edilen yükseklik ya da genişliğin yüzde 50'si 
50vw; doküman içinde nerde olursa olsun tam ekran genişliğinin yarısı
100vh; tam ekran yüksekliği
1rem: %100 percentage of relative to root element (html element) font size (default 16px)
1em: %100 percentage of parent font size relatively

vw = view-width
vh = view-hight
px = pixel
em = 
rem = relative 
fr = fraction


Use **em** for media queries.
https://zellwk.com/blog/media-query-units/

Don't use **em** for media queries
https://adamwathan.me/dont-use-em-for-media-queries/

