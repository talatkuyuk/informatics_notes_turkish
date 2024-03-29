# Styling React Components (React Component'lere Style Verme) Notları

React Component'lere pek çok stil verme yöntemi bulunmaktadır.

- in-line styling
- bir css dosyası import etme
- styled-components paketini kullanma
- module.css yöntemi
- bootstarap paketi _(buraya dahil edilmedi)_
- tailwind paketi _(buraya dahil edilmedi)_
- _ve diğerleri v.b._

## In-line styling

- Bu yöntemde Component içinde tanımlanan html elemanı için **style** parametresi kullanılır.
- HTML elemanının style parametresi `{key: value, ...}` şeklinde bir javascript objesi alır.
- JSX içinde html kodlarının içindeki javascript kodu {} içerisine alındığı için `style={{key1: value1, key2: value2}}` şeklinde çift _curly brace_ kullanılmış olur.
- Söz konusu Javascript objesi içindeki key'ler css attribute'leridir, ancak bu attribute'ler css'de belirtildiği gibi değil arasında dash(tire) olmadan ikinci kelimenin ilk harfi büyük olacak şekilde belirtilir. Eğer css'deki gibi belirtilmek isteniyorsa key'ler tırnak "" içerisine alınır.

```javascript
const App = () => {
  return (
    <div
      style={{
        width: "90%",
        border: "1px solid #ccc",
        maxWidth: "40rem",
        backgroundColor: "rgba(0, 0, 0, 0.2)",
        padding: "1rem",
      }}
    >
      <MyComponent />
    </div>
  );
};

// veya / or

const App = () => {
  return (
    <div
      style={{
        width: "90%",
        border: "1px solid #ccc",
        "max-width": "40rem",
        "background-color": "rgba(0, 0, 0, 0.2)",
        padding: "1rem",
      }}
    >
      <MyComponent />
    </div>
  );
};
```

- App render edilip html source'a bakıldığında <div style="width: 90%, ..."> şeklinde in-line olarak style parametresinin tanımlandığını görürüz.
- in-line styling basit bir kullanım ortaya sunar ama bazı dezavantajları vardır:
  - Css'nin doğal olarak sunduğu cascading özelliğinden faydalanamayız. Yani örneğin button DOM objesi için üst component'lerde tanımlanan bir stili alt componentlerde yer alan bir button için kullanamamış oluruz.
  - Pseudo elements ve pseudo selector'leri (örneğin :hover gibi) kullanamayız.
  - Media Query kullanamayız.
  - JSX kodu içinde yani bir javascript kodu içerisinde css görmek kodumuzu şişirebilir.
- Eğer, basit bir sayfa, uygulama yapılacaksa, pseudo selector vb. kullanılmayacaksa in-line styling tercih edilebilir, ama proje karmaşıklaştıkça sıkıntı yaratır.

## Bir css dosyası import etme

Burada bir css dosyası yaratılır ve projeye import edilir.

```javascript
// Button.css
button { color: white; }
button:hover { cursor: pointer; }
// React Component
import React from "react"
import "./Button.css"
const Button = props => {
    return <Button onClick={props.onClick}>{props.children}</Button>
}
```

- Bu sayede JSX içinde css kodları yer almamış olur.
- Ancak burada javascript, css kodunu gerçekte import etmez, react ile beraber çalışan webpack eklentisi sayesinde css kodu uygun şekilde render edilen html sayfası içine enjekte edilir, yerleştirilir.
- Css dosyasında yukarıda olduğu gibi genel bir type/tag seçici kullanılırsa (button), aynı sayfada render edilen ne kadar component varsa, bunlardaki buttonlar da etkilenir, hatta bu componentlerdeki buttonlar için bir stil belirtilmemiş olsa bile etkilenirler. Dolayısıyla bu componente özel bir css yazmış olmayız. Bu nedenle en azından class property'sini kullanmamız gerekir.
- Javascript dilinde **class** kelimesi reserved olduğundan class property için **className** property ismi kullanılılmaktadır. `<Button className="primaryButton" ...`

```javascript
// Button.css
.primaryButton { color: white; }
.primaryButton:hover { cursor: pointer; }
// React Component
import React from "react"
import "./Button.css"
const Button = props => {
    return <Button className="primaryButton" onClick={props.onClick}>{props.children}</Button>
}
```

- Class ismi belirtilse de tüm componentleri düşünerek ve ayrıştırarak farklı class isimleri vermek gerekebilir. Proje büyüdükçe bu durum sıkıntılı hale gelebilir.
- Farklı class isimleri vermek için örneğin BEM (Block Element Modifier) convention (kısaltma) yöntemi kullanılabilir. Bu yöntem sayesinde, proje boyunca bir class isminden yalnızca bir defa verildiği sağlanmış olur. Detay için bakınız: google

## Styled Components Paketi

https://styled-components.com

Söz konusu `styled-components` paketini kullanmak için paketi install edelim:

> npm install --save styled-components

Söz konusu paketi projemize dahil edelim:

> import styled from 'styled-components'

Bir styled button yaratalım. Burada <styled.button> paket içerisinde JSX komutları üreten bir fonksiyondur, button tipinde DOM objesi yaratmaktadır. İki backtick ise javascript'e ait bir feature olan <tagged template literal> adında kullanımdır. Bu sayede fonksiyona template literal gönderilmekte, javascript bunu ve içindeki interpolation string'leri **>{}** pars etmekte ve fonksiyonu öyle çağırmaktadır.

```javascript
const Button = styled.button``;
```

Bu button'un stilini backtick içerisinde belirteceğiz. Dikkat: normal css property'leri css dosyasında olduğu gibi aynen belirtebiliyoruz. (Tırnaklar yok, sonunda noktalı virgüller var.)

```javascript
const Button = styled.button`
  background: transparent;
  border-radius: 3px;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: 0 1em;
  padding: 0.25em 1em;
`;
```

Bu styled butona parametre gönderebiliyoruz. Bu parametreleri **props** ile alıyoruz, backtick içinde olduğumuz için javascript komutlarını **>{}** içinde kullanıyoruz (interpolation). `>{props => javascript command for props.something}`. Bu javascript içinde tekrar css property'leri belirtmek için de styled paketinde yer alan css fonksiyonunu **css``** kullanıyoruz.

Aşağıdaki örnekte styled bir button ve styled div oluşturulmuştur.

```javascript
import styled, { css } from 'styled-components'

const Button = styled.button`
  background: transparent;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: 0.5em 1em;
  padding: 0.25em 1em;

  border-radius: >{props => props.primary ? "3px" : "2px"};

  >{props => props.primary && css`
    background: palevioletred;
    color: white;
  `}

  :hover {
      outline: none;
      color: lightblue;
  }
`;

const Container = styled.div`
  text-align: center;
`

render(
  <Container>
    <Button onClick={}>Normal Button</Button>
    <Button primary>Primary Button</Button>
  </Container>
);
```

- App render edilip html source'a bakıldığında <button class="sc-bDDvas ErkjjY"> şeklinde sınıflar yaratıldığını, bu sınıflara ait css tanımlamalarında (html head içerisinde) girdiğimiz ilgli css parametrelerini görürüz.
- styled-components bize esneklik ve dinamiklik sunmaktadır.
- styled component içinde css'yi olduğu gibi kullanabilmekteyiz. (Media Query, psuedo selectors, pseudo elements vb. normal css'de olduğu gibi hatta scss'ye benzeyen nested yapıda)
- styled component içinde de kullanabilmekteyiz.
- yaratılan styled component programın her yerinde aynı şekilde kullanılabilmektedir.

Örnek styled bir paragraph yaratalım, başka bir dosyada import ederek kullanalım.

```javascript
import styled from "styled-components"
const StyledParagraph = styled.p`
  color: >aaa;

  > strong {
    font-weight: bold;
  }

  @media (min-width: 760px) {
    color: >fff;

    > strong {
        font-weight: normal;
    }
  }
`
export default StyledParagraph;

import StyledParagraph from "path-to-StyledParagraph"
const MyComponent = () {
    return (
        <StyledParagraph> My Color is <strong> mine </strong> </StyledParagraph>
    )
}
```

## module.css yöntemi

Bir css dosyası yaratılıp, component'e (JSX dosyasına) import edilmesinin, diğer componentleri etkileyebileceğini söylemiştik.
İşte buna çözüm olarak, yani css dosyasının o componente özel olmasını sağlamak için **module.css** yöntemi kullanılmaktadır.

```javascript
// Button.module.css
.primaryButton { color: white; }
.primaryButton:hover { cursor: pointer; }
// React Component
import React from "react"
import classes from "./Button.module.css"
const Button = props => {
    return <Button className={classes.primaryButton} onClick={props.onClick}>{props.children}</Button>
}
```

- Normal css dosyası için kullanılan `import from "./Button.css"` ile, module.css kullanıldığında `import classes from "./Button.module.css"`arasındaki değişikliğe dikkat.
- Normal css kullanıldığında Button içinde `className="primaryButton"` kullanımı ile, module.css kullanıldığında `className={classes.primaryButton}` kullanımına dikkat.
- css dosyası içindeki .primaryClass sınıf adı diğer css dosyalarında olsa bile, module.css sayesinde bu componente özel olarak kalabilmektedir. (class isimleri burada case sensitive'dir yani büyük küçük harfe duyarlıdır.)
- React ile beraber çalışan webpack eklentisi, build aşamasında bu module.css dosyalarını özel bir işlemden geçirerek, classları farklı isimlendirerek (örneğin _.Button_primaryButton\_\_2Ce79_ gibi) burada yazılı css sınıflarının bu componente özel olmasını sağlamaktadır.
- Eğer bir css dosyasının componente özel olmasını istiyorsak **module.css** yöntemini, componente özel değil tüm web sayfasına hakim olmasını istiyorsak **normal css import** yöntemini kullanmamız uygun olacaktır.
