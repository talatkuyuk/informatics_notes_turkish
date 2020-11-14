# Parcel Notları
Parcel paketi nodejs ekosistemi içinde yer alan "web application bundler" hizmeti sunan bir pakettir. Webpack'in yaptığı işi yapar, ama daha az dependency ve setting gerektirdiği söylenmektedir.

## Parcel'in Global olarak kurulumu
```powershell
> npm install -g parcel-bundler
```
Globally olarak yükledikten sonra komut satırından kullanabiliriz.
```powershell
> parcel index.html
```

## Parcel'in proje bazında kurulumu
React app oluşturmak için create-react-app paketini kullanıyorduk.
```powershell
> npx create-react-app project_name
```
Bu paket pek çok dependency (webpack bundler, babel etc.) yüklemekte ve kullanmasak bile büyük bir node_modules klasörü yaratmakta idi.

İşte bu duruma bir alternatif olarak **parcel bundler** kullanılmaktadır.
```powershell
> mkdir project_name
> cd project_name
> npm init -y # generates a working package.json for you
> npm install --save-dev parcel-bundler
> # npm i -D parcel-bundler
> npm install react react-dom
```
**in package.json**
```"start": "parcel index.html --open"```

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

ReactDOM.render(<h1>Hello world!</h1>, document.getElementById("root"))
```
Tüm bu ayarlardan sonra
```powershell
> npm start
```


