# React Hooks (useEffect) Notları

Genel olarak, component içinde bir API çağırmak için kullanılır.

## Projeye dahil etmek

```javascript
import React, { useEffect } from "react";
import React, { useState, useEffect } from "react";
import { useEffect } from "react";
```

## useEffect

useEffect parametre olarak bir fonksiyon alır. İlave ve optional (isteğe bağlı) olarak bir array de alabilirr.

Buradaki array parametresi "dependency" bağımlılık değişkenlerinin tutulduğu bir dizidir. Dizi boş olabilir, bir veya birden fazla değişken barındırabilir.

```javascript
const [count, setCount] = useState(() =>
  JSON.parse(localStorage.getItem("count"))
);

useEffect(() => {
  localStorage.setItem("count", JSON.stringify(count));
}, [count]);

return (
  <div>
    <div>count: {count}</div>
    <button onClick={() => setCount((c) => c + 1)}>increment</button>
  </div>
);
```

Dependency Array parametresi girilmeze, useEffect fonksiyonu her render işleminde çalışır.
It is like ComponentDidMount for Class Based Component.

```javascript
React.useEffect(() => {
  console.log("render");
});
```

Dependency Array parametresi boş bir dizi olarak girilirse sadece ilk mounting render işleminde icra edilir, diğer render işlemlerinde useEffect fonksiyonu çağrılmaz.

```javascript
React.useEffect(() => {
  console.log("render");
}, []);
```

Dependency Array parametresi dolu bir dizi ise dizide belirtilen her bir değişkenin değeri değiştiği anda useEffect fonksiyonu bir kez daha çağrılır.

```javascript
React.useEffect(() => {
  console.log("render");
}, [count, formElements.email]);
```

useEffect fonksiyonunda component unmount olurken bazı işlemlerin yapılması isteniyor ise return fonksiyonu kullanılır. Eğer dependency array'de belirtilen bir değişkenin değişmesi sonucu useEffect fonksiyonu yeniden çağrılırsa, component unmount olmasa da önceki useEffect fonksiyonun return fonksiyonu çağrılır (clean-up gibi bir şey), sonra useEffect fonksiyonu yerine getirilir.

```javascript
import React, { useEffect } from "react";

export const Hello = () => {
  useEffect(() => {
    console.log("render");

    return () => {
      console.log("unmount");
    };
  }, []);

  return <div>hello</div>;
};

import React, { useEffect, useState } from "react";
import { Hello } from "./Hello";

const App = () => {
  const [showHello, setShowHello] = useState(true);
  return (
    <div>
      <button onClick={() => setShowHello(!showHello)}>
        toggle show hello
      </button>
      {showHello && <Hello />}
    </div>
  );
};

export default App;
```

useEffect fonksiyonu window objesine listener eklemede de kullanılabilir.

```javascript
useEffect(() => {
  const onMouseMove = (e) => {
    console.log(e);
  };
  window.addEventListener("mousemove", onMouseMove);

  return () => {
    window.removeEventListener("mousemove", onMouseMove);
  };
}, []);
```

Birden fazla useEffect kullanılabilir. Bunlar peşi sıra icra edilir.

```javascript
useEffect(() => {
  console.log("mount1");
}, []);
useEffect(() => {
  console.log("mount2");
}, []);
```

useEffect kullanarak örneğin useFetch şeklinde bir custom hook yazabiliriz..

```javascript
import { useEffect, useState } from "react";

export const useFetch = (url) => {
  const [state, setState] = useState({ data: null, loading: true });

  useEffect(() => {
    setState((state) => ({ data: state.data, loading: true }));
    fetch(url)
      .then((x) => x.text())
      .then((y) => {
        setState({ data: y, loading: false });
      });
  }, [url, setState]);

  return state;
};

import React, { useEffect, useState } from "react";
import { useFetch } from "./useFetch";

const App = () => {
  const [count, setCount] = useState(() =>
    JSON.parse(localStorage.getItem("count"))
  );
  const { data, loading } = useFetch(`http://numbersapi.com/>{count}/trivia`);

  useEffect(() => {
    localStorage.setItem("count", JSON.stringify(count));
  }, [count]);

  return (
    <div>
      <div>{!data ? "loading..." : data}</div>
      <div>count: {count}</div>
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
    </div>
  );
};

export default App;
```
