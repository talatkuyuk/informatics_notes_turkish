## Styled Components (styled-components)
Styled Components, React component eko sistemi içerisinde css'nin esnek ve dinamik şekilde kullanılmasını sağlayan bir pakettir.

**Resourse:** https://styled-components.com

**styled-components** paketinin kurulması:
> npm install --save styled-components

**styled-components** paketinin projeye dahil edilmesi:
> import styled from 'styled-components'

styled-components paketi, CSS syntax'ının JSX içerisinde yer almasını sağlayan ve HTML elemanlarını yaratan JSX kodlarını üreten fonksiyonlar içermektedir. Örneğin:
```javascript
styled.button
styled.p
styled.img
styled.css
```

Bu fonksiyonlar, parametrelerini **function()** şeklinde değil **function``** şeklinde almaktadır.
```javascript
styled.button``
styled.p``
styled.img``
styled.css``
```

İki backtick <Tagged Template Literal> adında javascript'e ait bir ES6 feature'dur.  Bu sayede fonksiyona <template literal> gönderilmekte, javascript bunu ve içindeki *interpolation*'ları pars etmekte ve fonksiyonu öyle çağırmaktadır. *Bactick içinde **${}** kullanımı*

> *Tagged Template Literal içinde javascript interpolation:* string içinde javascript kodu olmasıdır. javascript kodu ${} içinde yazılır, ancak string normal tırnak değil backtick içinde olmalıdır. Örnek : `This string includes some interpolations: ${key} ve ${()=> a+b;} `

Örneğin aşağıda <styled.button> bir fonksiyondur, button tipinde DOM objesi yaratan JSX kodu üretmektedir. Bu button'un stilini backtick içerisinde belirteceğiz. *Dikkat: css property'leri normal css dosyasında olduğu gibi aynen belirtebiliyoruz. (Tırnaklar yok, sonunda noktalı virgüller var.)*
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
Bu styled butona parametre gönderebiliyoruz. Bu parametreleri **props** ile alıyoruz, backtick içinde olduğumuz için javascript komutlarını **${}** içinde kullanıyoruz (interpolation). ```${props => javascript command for props.something}```. Bu javascript içinde tekrar css property'leri belirtmek için de styled paketinde yer alan css fonksiyonunu **css``** kullanıyoruz.

Aşağıdaki örnekte styled bir button ve styled div oluşturulmuştur.
```javascript
import styled, { css, keyframes } from 'styled-components'
const fadeIn = keyframes`
    0% { opacity: 0; }
    100% { opacity: 1; }
`
const Button = styled.button`
  background: transparent;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: ${props => props.margin || "2rem"};
  padding: 0.25em 1em;

  border-radius: ${props => props.primary ? "3px" : "2px"}; // yöntem-1: props
  border-radius: ${{primary} => primary ? "3px" : "2px"}; // yöntem-2: destruction

  animation: 2s ${fadeIn} ease-in;

  ${props => props.primary && css`
    background: palevioletred;
    color: white;
  `}

  :hover {
      outline: none;
      color: lightblue;
  }

  // diğer styled componenti etkileme
  ${Container}:hover {
      color: red;
  }
`;

const Container = styled.div`
  text-align: center;

  // diğer styled componenti etkileme
  &:hover ${Button} {
      color: red;
  }
`

render(
  <Container>
    <Button onClick={}>Normal Button</Button>
    <Button primary>Primary Button</Button>
  </Container>
);
```
+ App render edilip html source'a bakıldığında <button class="sc-bDDvas ErkjjY"> şeklinde sınıflar yaratıldığını, bu sınıflara ait css tanımlamalarında (html head içerisinde) girdiğimiz ilgli css parametrelerini görürüz.
+ styled-components bize esneklik sunmaktadır.
+ styled içinde psuedo selector'leri normal css'de olduğu gibi hatta scss'ye benzeyen nested yapıda kullanabilmekteyiz.
+ yaratılan styled component, import edildiği programın her yerinde aynı şekilde kullanılabilmektedir. 


Örnek bir styled paragraph yaratalım, başka bir dosyada import ederek kullanalım.
```javascript
// StyledParagraph.js
import styled from "styled-components"
const StyledParagraph = styled.p`
  color: $aaa;
`
export default StyledParagraph;
// main.js
import StyledParagraph from "path-to-StyledParagraph"
const MyComponent = () {
    return (
        <StyledParagraph> My Color is #aaa </StyledParagraph>
    )
}
```

Örnek bir styled div yaratalım, başka bir dosyada import ederek kullanalım.
```javascript
// Wrapper.js
import styled from "styled-components"
export default styled.div`
  margin: 0;
  padding: 30px;

  p {
      font-size: 1rem;
  }

  & .big {
      font-size: 2rem;
  }
`
// main.js
import Wrapper from "path-to-Wrapper"
cons name = "ipikuka"
const MyComponent = () {
    return (
        <Wrapper>
            <p>My Name is {name}</p>
            <p className="big">My big Name is {name}</p>
        </Wrapper>
    )
}
```

Styled Fonksiyonu ve Component aynı dosyada da yer alabilir.
```javascript
// App.js
import styled from "styled-components"
const Wrapper = styled.div`
  margin: 0;
  padding: 30px;
`
const MyComponent = () {
    return (
        <Wrapper>
            <p>My Name is {name}</p>
        </Wrapper>
    )
}
```

Örnek bir styled component daha:
```javascript
// Button.js
import React from "react"
import styled from "styled-components"
const StyledButton = styled.button`
  font-size: 2rem;
  color: ${props => props.primary ? "red" : "#fff"}; 
`
const Button = ({ children, primary}) {
    return (
        <StyledButton primary={primary}>
            { children }
        </StyledButton>
    );
}
export default Button;

// App.js'deki import satırı ve Button isimli styled componentin çağrılması
import Button from "path-to-Button"
<Button primary>My Button</Button>
```

**attrs fonksiyonu**
Örneğin styled bir a DOM objesi oluşturan Link isminde bir styled component yaratalım. Bütün a'lar target="_blank" ise bunu Link'e taşıyabiliriz. 
```javascript
// const Link = styled.a``
// const Link = styled.a.attrs()``
const Link = styled.a.attrs(props=>{
    target = "_blank"
})`
    color: violet;
    font-size: 1rem;
`
const MyApp = () => {
    return (
        <>
            // Link'te target prop'unu yazmaya gerek kalmadı.
            <Link href="www.gooogle.com">
                Link to google
            </Link> 
        </>
    )
}

```


Bir styled component'in tagged template literal içerisinde **${}** kullanarak her türlü javascript kodunu yazabiliriz.
```javascript
const PaginationWrapper = styled.div`
  display: flex;
  width: 100%;
  justify-content: ${ props =>
    if (page === "first") return "flex-end"
    else if (page === "middle") return "space-between"
    else return "flex-start"
  }
`
const MyPaginationComponent = () => {
    let page_description = some-logic-to-if-current-page-is-first-middle-last
    <PaginationWrapper page={page_description}>
        {some-logic-if-Prev-Button-is-Needed}
        <Button>Prev<Button>
        {some-logic-if-Next-Button-is-Needed}
        <Button>Next<Button>
    </PaginationWrapper>
}

```

## Extending the styled component
Bir styled component'i ```styled() constructor``` ile inherit ederek başka bir styled component yaratabiliriz. Yeni özellikler ekleyerek ya da mevcut özellikleri override yaparak extend edebiliriz.
```javascript
// App.js
const SuperStyledButton = styled(StyledButton)`
  font-size: 2.5rem;
  color: ${props => props.primary ? "red" : "#fff"}; 
`
```



Styled Components paketi bize bir **Theme Provider** sunmaktadır. Theme Provider, bir react context API sağlamakta ve theme objesini etki alanındaki tüm componentlere ulaştırmaktadır. Dolayısıyla örneğin **HeaderText** componenti **theme** bilgisine ulaşabilmektedir.
```javascript
// App.js
import React from "react"
import { ThemeProvider } from "styled-components"
import Wrapper from "./components/Wrapper"
import HeaderText from "./components/HeaderText"
const theme = {
    font: "calibri"
}
export default () => {
    <ThemeProvider theme={theme}>
        <Wrapper>
            <HeaderText>I am the Header</HeaderText>
            <p>My Name is {name}</p>
        </Wrapper>
    </ThemeProvider>
}

// HeaderText.js
import styled from "styled-components"
const HeaderText = styled.h1`
  font-family: ${props => props.theme.font};
`
```

+ Birden fazla **theme** objesi yaratabiliriz. Theme objesinin içerisinde css attribute şeklinde key'ler kullanmak zorunda değiliz. ThemeProvider'ın sağladığı theme propunu ilgili styled component içinde ```props.theme.anyKey``` şeklinde karşılamamız gerekir.
+ Birden fazla ve farklı theme propu kullanan **Theme Provider** kullanabiliriz. Theme Provider sadece kapsadığı componentlerde geçerlidir. **Hatta ThemeProvider'lar nested bile olabilir.**
```javascript
// App.js
import React from "react"
import { ThemeProvider } from "styled-components"
import Wrapper from "./components/Wrapper"
import HeaderText from "./components/HeaderText"
const theme1 = { anyKey: "calibri" }
const theme2 = { anyKey: "arial" }
export default () => {
    <Wrapper>
        <ThemeProvider theme={theme1}>
            <HeaderText>I am the Header</HeaderText>
            <p>My Name is {name}</p>
        </ThemeProvider>
        <ThemeProvider theme={theme2}>
            <HeaderText font="arial">I am the Header</HeaderText>
            <p>My Name is {name}</p>
        </ThemeProvider>
    </Wrapper>
}
// HeaderText.js
import styled from "styled-components"
const HeaderText = styled.h1`
  font-family: ${props => props.font ? props.font : props.theme.anyKey};
`
```

**defaultProps** ile styled componente *default theme* atayabiliriz. Örneğin aşağıdaki buton, *ThemeProvider kapsama alanında ise* provider'ın sağladığı theme'den, *kapsama alanında değilse* defaultProps'un sağladığı theme'den bilgileri alacaktır.
```javascript
const Button = styled.button`
  font-size: 1em;
  color: ${props => props.theme.main};
  border: 2px solid ${props => props.theme.main};
`;
Button.defaultProps = {
  theme: {
    main: "palevioletred"
  }
}
```

ThemeProvider'ın theme propuna bir fonksiyon da atayabiliriz. Örneğin aşağıda Theme objesini alıp içindeki key value parametrelerini yer değiştiren *invertTheme* adında bir fonksiyon tanımlanmıştır. Ayrıca ThemeProvider için nested bir örnek sunulmuştur.
```javascript
const Button = styled.button`
  color: ${props => props.theme.fg};
  border: 2px solid ${props => props.theme.fg};
  background: ${props => props.theme.bg};
  font-size: 1em;
`;

const theme = {
  fg: "palevioletred",
  bg: "white"
};

// key value parametrelerini yer değiştiren fonksiyon
const invertTheme = ({ fg, bg }) => ({
  fg: bg,
  bg: fg
});

render(
  <ThemeProvider theme={theme}>
    <div>
      <Button>Default Theme</Button>

      <ThemeProvider theme={invertTheme}>
        <Button>Inverted Theme</Button>
      </ThemeProvider>
    </div>
  </ThemeProvider>
);
```

ThemeProvider'ın sağladığı theme propuna *styled component dışından da* ulaşabiliriz. Bunun için iki yöntem vardır: 
+ **1)** styled-components paketinin sağladığı *withTheme* ile 
+ **2)** react'ın kendi sağladığı *useContext* hook kullanarak styled-components paketinin sağladığı *ThemeContext* ile
```javascript
// class component
import { withTheme } from 'styled-components';
class MyComponent extends React.Component {
  render() {
    console.log('Current theme: ', this.props.theme);
    // ...
  }
}

// function component
export default withTheme(MyComponent);
import { withTheme } from 'styled-components';
const MyComponent = () => {
  return {
    console.log('Current theme: ', this.props.theme);
  }
}
export default withTheme(MyComponent);

// useContext Hook ile
import { useContext } from 'react';
import { ThemeContext } from 'styled-components';
const MyComponent = () => {
  const themeContext = useContext(ThemeContext);
  console.log('Current theme: ', themeContext);
  // ...
}
```

**The theme prop**

Theme objesini ThemeProvider kullanmadan da ilgili styled componente theme propu ile gönderebiliyoruz. Theme propu bir object kabul ettiği için çift curly brace kullandığımıza dikkat edelim. **theme={{ key: value, ...}}** Ayrıca ThemeProvider'ın kapsama alanındaki styled component'in theme propu ile ThemeProvider'ın sağladığı theme üzerine override yazılabilir. 
```javascript
// Define our button
const Button = styled.button`
  font-size: 1em;
  color: ${props => props.theme.main};
  border: 2px solid ${props => props.theme.main};
`;

const theme = {
  main: "mediumseagreen"
};

render(
  <div>
    <Button theme={{ main: "royalblue" }}>Ad hoc theme</Button>
    <ThemeProvider theme={theme}>
      <div>
        <Button>Themed</Button>
        <Button theme={{ main: "darkorange" }}>Overridden</Button>
      </div>
    </ThemeProvider>
  </div>
);
```