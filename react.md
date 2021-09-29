# React Notları


## React App Oluşturulması
```powershell
# project_name adında klasör oluşturur
> npx create-react-app project_name

# eğer zaten proje klasörü içinde isek
> npx create-react-app ./

> npx create-react-app project_name --template [template-name]
> npx create-react-app project_name --template clean-cra // test ve servisworkerın kaldırılmış hali
> npx create-react-app project_name --template redux   // redux-toolkit kullanıyor

dene bu ikisini
> npx create-react-app project_name --template cra-template-so-toolkit
> npx create-react-app project_name --template cra-template-so-riridux
```
Bu komut bulunulan klaörün içinde React Application oluşturur ve projeye ait bir klasör yaratır.

npx'in npm'den farkı ilgili paketi bilgisayara kurmadan çalıştırmasıdır.

> İki tip React Component var : **Functional** or **Class-based**<br>
> Son dönemde *Functional* olan tercih ediliyor, burada *Hook*'lar kullanılıyor.

Güzel bir başlangıç noktası: [Academind Tutorial](https://academind.com/learn/react/react-hooks-introduction/) Bu makale aynı zamanda React Hook orjinal kaynaklarına linkler içermektedir.

## React App'in Başlatılması
```powershell
> npm start
```

## JSX
```javascript
import React from "react"
import './App.css';

const name = "ipikuka"

const App = () => {
    return <div>Hello {name} </div>;
}
export default App
```

## Firebase'i projeye eklemek ve package.json'a kaydetmek için
```powershell
> npm install --save firebase
```

## Firebase'i projeye eklemek için
Web Setup İşlemleri için [kendi sitesi](https://firebase.google.com/docs/web/setup).
Örnek bir [code labaratuvarı]().

**Removing Unused React Imports**
```powershell
cd your_project
npx react-codemod update-react-imports
```

## react wşth redux-toolkit
npm i react react-dom redux react-redux @reduxjs/toolkit


## production server yaratma
--------------
npx serve (dist içindeyken)
npx serve foldername
npx serve dist

npx http-server [path] [options]


## kısa yollar (ES7 React/Redux/GraphQL/RN snippets extension)
rafce   react arrow function component export
