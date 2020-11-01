# Styling React Components (React Component'lere Style Verme) Notları
React Component'lere pek çok stil verme yöntemi bulunmaktadır. Bunlardan üç tanesi ön plana çıkmaktadır.
+ in-line styling
+ normal css dosyası yaratıp import etme
+ styled-components paketini kullanma
+ module.css yöntemi


## In-line styling
+ Bu yöntemde Component içinde tanımlanan html elemanı için **style** parametresi kullanılır.
+ HTML elemanının style parametresi ```{key: value, ...}``` şeklinde bir javascript objesi alır. 
+ JSX içinde html kodlarının içindeki javascript kodu {} içerisine alındığı için ```style={{key1: value1, key2: value2}}``` şeklinde çift *curly brace* kullanılmış olur.
+ Söz konusu Javascript objesi içindeki key'ler css attribute'leridir, ancak bu attribute'ler css'de belirtildiği gibi değil arasında dash(tire) olmadan ikinci kelimenin ilk harfi büyük olacak şekilde belirtilir. Eğer css'deki gibi belirtilmek isteniyorsa key'ler tırnak "" içerisine alınır.

```javascript
const App = () => {
    return (
        <div 
            style={{
                width: "90%",
                border: "1px solid #ccc",
                maxWidth: "40rem",
                backgroundColor: "rgba(0, 0, 0, 0.2)",
                padding: "1rem"
            }}
        >
            <MyComponent />
        </div>
    );
}

// veya / or

const App = () => {
    return (
        <div 
            style={{
                "width": "90%",
                "border": "1px solid #ccc",
                "max-width": "40rem",
                "background-color": "rgba(0, 0, 0, 0.2)",
                "padding": "1rem"
            }}
        >
            <MyComponent />
        </div>
    );
}
```
+ App render edilip html source'a bakıldığında <div style="width: 90%, ..."> şeklinde in-line olarak style parametresinin tanımlandığını görürüz.
+ in-line styling basit bir kullanım ortaya sunar ama bazı dezavantajları vardır:
    + Css'nin doğal olarak sunduğu cascading özelliğinden faydalanamayız. Yani örneğin button DOM objesi için üst component'lerde tanımlanan bir stili alt componentlerde yer alan bir button için kullanamamış oluruz.
    + Pseudo elements ve pseudo selector'leri (örneğin :hover gibi) kullanamayız.
    + JSX kodu içinde yani bir javascript kodu içerisinde css görmek kodumuzu şişirebilir.
+   Eğer, basit bir sayfa, uygulama yapılacaksa, pseudo selector vb. kullanılmayacaksa in-line styling tercih edilebilir, ama proje karmaşıklaştıkça sıkıntı yaratır. 


## Styled Components Paketi
https://styled-components.com

Söz konusu ```styled-components``` paketini kullanmak için paketi install edelim:
> npm install --save styled-components

Söz konusu paketi projemize dahil edelim:
> import styled from 'styled-components'

Bir styled button yaratalım
> const Button = styled.button``

Bu button'un stilini backtick içerisinde belirteceğiz. Dikkat: normal css property'leri css dosyasında olduğu gibi aynen belirtebiliyoruz. (Tırnaklar yok, sonunda noktalı virgüller var.)
```javascript
const Button = styled.button`
  background: transparent;
  border-radius: 3px;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: 0 1em;
  padding: 0.25em 1em;
`
```
Bu styled butona parametre gönderebiliyoruz. Bu parametreleri **props** ile alıyoruz, backtick içinde olduğumuz için javascript komutlarını **${}** içinde kullanıyoruz. ```${props => javascript command for props.something}```. Bu javascript içinde tekrar css property'leri belirtmek için de styled paketinde yer alan css fonksiyonunu **css``** kullanıyoruz.
```javascript
import styled, { css } from 'styled-components'

const Button = styled.button`
  background: transparent;
  border-radius: 3px;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: 0.5em 1em;
  padding: 0.25em 1em;

  ${props => props.primary && css`
    background: palevioletred;
    color: white;
  `}
`;

const Container = styled.div`
  text-align: center;
`

render(
  <Container>
    <Button>Normal Button</Button>
    <Button primary>Primary Button</Button>
  </Container>
);
```