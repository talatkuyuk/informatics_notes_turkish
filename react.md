# React Notları


## React App Oluşturulması
```powershell
> npx create-react-app project_name
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