# Parcel Bundler Notları
Parcel paketi, **nodejs** ekosistemi içinde yer alan **"web application bundler"** hizmeti sunan bir pakettir. 

**Parcel** bir bundler'dır. Webpack'in yaptığı işi yapar, ama daha az dependency ve setting gerektirdiği söylenmektedir. Snowpack gibi başka bundler'lar da vardır.

**Babel** bir transpiler'dır. Javascript kodunu pure javascripte çevirir. Typescript de bir transpiler'dır.

**https://createapp.dev/**
Browser üzerinden web application oluşturmamızı sağlayan bir sitedir. 


## Parcel'in Global olarak kurulumu
```powershell
> npm install -g parcel-bundler
```
Global olarak yükledikten sonra parcel'i *entry point* belirterek komut satırından kullanabiliriz. 
```powershell
> parcel index.html 
```
Defult sever http://localhost:1234/ adresidir. Port numarasını kendimiz de belirtebiliriz.
```powershell
> parcel index.html -p 3000
```
--open parametresi ??


## Parcel'in proje bazında kurulumu
React app oluşturmak için create-react-app paketini kullanıyorduk. Bu paket pek çok dependency (webpack bundler, babel etc.) yüklemekte ve bazı paketleri kullanmasak bile büyük bir node_modules klasörü yaratmakta idi.
```powershell
> npx create-react-app project_name
```


İşte bu duruma bir alternatif olarak **parcel bundler** kullanılmaktadır.
```powershell
> mkdir project_name
> cd project_name
> npm init -y # package.json üretir.
> npm install --save-dev parcel-bundler
> # npm i -D parcel-bundler
> npm install react react-dom
```
**in package.json** if no use any framework
```javascript
  "scripts": {
    "clean": "rm dist/bundle.js",
    "dev": "parcel src/index.html",
    "build": "parcel build src/index.html --public-url ./"
  },
  "dependencies": {},
  "devDependencies": {
    "parcel-bundler": "^1.12.4",
    "@babel/core": "^7.12.3",
    "@babel/preset-env": "^7.12.1"
  }
```

**in package.json** if use React framework
```javascript
  "scripts": {
    "clean": "rm dist/bundle.js",
    "dev": "parcel src/index.html",
    "build": "parcel build src/index.html"
  },
  "dependencies": {
    "react": "^17.0.1",  //add
    "react-dom": "^17.0.1"  //add
  },
  "devDependencies": {
    "parcel-bundler": "^1.12.4",
    "@babel/core": "^7.12.3",
    "@babel/preset-env": "^7.12.1",
    "@babel/preset-react": "^7.12.5" //add
  }
```

**index.html**
```html
<body>
    <div id="root"></div>
    <script src="src/index.js"></script>
</body>
```
**src/index.js**
```javascript
import React from "react"
import ReactDOM from "react-dom"

ReactDOM.render(
  <h1>Hello world!</h1>, 
  document.getElementById("root")
)
```
Tüm bu ayarlardan sonra
```powershell
> npm run start
```

## Sass Eklemek
Parcel çalıştırıldığında projede Saas olduğunu anlar, kendisi Saas paketini otomatik olarak indirir. Ama manuel olarak kurulmak isteniyorsa:
```powershell
> npm i -D saas
```

Parcel sitesinde, .sassrc adında bir file yaratılması ve aşağıdaki ayarların kaydedilmesi önerilmektedir. (This file controls the sass compilation with Parcel.) 
```javascript
{
  "includePaths": ["node_modules"],
  outputStyle: "nested",
}
```
Şu şekilde kullanılır.Dependencies in the SCSS files can be used with the @import statements.
```javascript
import './custom.scss' // in js file
<link rel="stylesheet" href="./style.scss">  // or from html file
```


## Babel paketini manuel olarak ayarlamak
Babel, javascript kodunu genel olarak plugin ve presetleri kullanarak transpile etmektedir. React için kullanılacak preset: @babel/preset-react
```powershell
> npm i -D @babel/core @babel/preset-env @babel/preset-react
```
**in .babelrc**
```javascript
// If you are using @babel/preset-react
{
  "presets": [
    ["@babel/preset-react", {
      "runtime": "automatic"
    }]
  ]
}
```

Hazır bir preset yerine pluginleri kendimiz de belirleyebilirz. JSX kodunu transfor eden plugin:
@babel/plugin-transform-react-jsx

**in .babelrc**
```javascript
// If you're using @babel/plugin-transform-react-jsx
{
  "plugins": [
    ["@babel/plugin-transform-react-jsx", {
      "runtime": "automatic"
    }]
  ]
}
```
## Styled Components Ayarı
Javascript kodu transpile edildiğinde html elemanının class isminin içinde styled component ismini de içermesi için aşağıdaki plugin kullanılır.
```powershell
> npm install babel-plugin-styled-components
```
**in .babelrc**
```javascript
{
  "plugins": ["babel-plugin-styled-components"]
}
```

## ESLint Ayarı
Yazdığımız kodlardaki hata ve önerileri bulmamıza yardımcı olan ESLinti projeye dahil edelim. İki paket gerekli.
```powershell
> npm i -D eslint eslint-plugin-react
```

```javascript
{
  // React 1.7'den itibaren aşağıdaki kurallar silinebilir veya off edilebilir. Çünkü JSX'i transform etmek için React 1.7 gerekmiyor artık.
  "rules": {
    // ...
    "react/jsx-uses-react": "off",
    "react/react-in-jsx-scope": "off"
  }
}
```

