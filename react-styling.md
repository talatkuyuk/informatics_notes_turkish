# Styling React Components (React Component'lere Style Verme) Notları
React Component'lere pek çok stil verme yöntemi bulunmaktadır. Bunlardan üç tanesi ön plana çıkmaktadır.
+ in-line styling
+ styled-components paketini kullanma
+ module.css yöntemi


## In-line Styling Components
+ Bu yöntemde Component içinde tanımlanan html elemanı için **style** parametresi kullanılır.
+ HTML elemanının style parametresi ```{key: value, ...}``` şeklinde bir java script objesi alır. 
+ JSX içinde html kodlarının içindeki javascript kodu {} içerisine alındığı için ```style={{key1: value1, key2: value2}}``` şeklinde çift *curly brace* kullanılmış olur.
+ Söz konusu Javascript objesi içindeki key'ler css attribute'leridir, ancak bu attribute'ler css'de belirtildiği gibi değil arasında dash(tire) olmadan ikinci harf büyük olacak şekilde belirtilir. Eğer css'deki gibi belirtilmek isteniyorsa key'ler tırnak "" içerisine alınır.

```javascript
const App = () => {
    return (
        <div 
            style={{
                border: "1px solid #ccc",
                width: "90%",
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
                "border": "1px solid #ccc",
                "width": "90%",
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

## Styled Components
xxxxr.