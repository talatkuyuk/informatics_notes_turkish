# Styling React Components (React Component'lere Style Verme) Notları
React Component'lere pek çok stil verme yöntemi bulunmaktadır. Bunlardan üç tanesi ön plana çıkmaktadır.
+ In-line Styling Components
+ styled-components paketini kullanma
+ module.css yöntemi


## In-line Styling Components
+ Bu yöntemde Component içinde tanımlanan html elemanları için **style** parametresi kullanılır.
+ HTML elemanının style parametresi ```{key: value}``` şeklinde bir java script objesi alır. 
+ JSX içinde html kodlarının içindeki javascript kodu {} içerisine alındığı için ```style={{key1: value1, key2: value2}}``` şeklinde çift *curly brace* kullanılmış olur.
+ Style tanımlayan Javascript objesi içindeki key'ler html attribute'lerdir, ancak bu attribute'ler css'de belirtildiği gibi değil arasında dash(tire) olmadan ikinci harf büyük olacak şekilde belirtilir. Eğer css'deki gibi belirtilmek isteniyorsa key'ler tırnak "" içerisine alınır.

```javascript

```

## Styled Components
xxxxr.