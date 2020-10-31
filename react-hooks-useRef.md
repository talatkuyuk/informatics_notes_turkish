# React Hooks (useRef) Notları
Genel olarak, bir Virtual DOM objesini referans etmek, component içinde state'i değiştirmeyecek şekilde bir değişkeni kontrol etmek, bir fonksiyon çağırmak vb. için kullanılmaktadır.

useRef değişkeninin değeri değiştiğinde useState'ten farklı olarak re-render gerçekleşmez. Yani durum değişmez.

## Projeye dahil etmek
```javascript
import React, { useRef } from "react"
import { useRef } from "react"
```

## useRef
useRef bir parametre alması opsiyoneldir.
Eğer bir Virtual DOM objesini refere edecekse paramatre almasına gerek yoktur.
Eğer bir değişken veya fonksiyon barındıracaksa bunu parametre olarak alır.

useRef refere ettiği VirtualDOM objesini veya değer/fonksiyonu döndürür.

Aşağıdaki örnekte **useRef()**, bir Virtual DOM objesini refere etmektedir. 
```javascript
const App = () => {
  const inputRef = useRef();
  return (
    <div>
        <input ref={inputRef} name="email"/>
        <button onClick={() => { 
            inputRef.current.focus(); 
            inputRef.current.style.backgroundColor = "red";
        }} > focus and make red </button>
    </div>
  );
};
```

Aşağıdaki örnekte **useRef(function)**, bir fonksiyonu refere etmektedir.
```javascript
const App = () => {
  const helloRef = useRef(() => console.log("hello"));
  return (
    <div>
        <button onClick={() => { helloRef.current(); }} > focus </button>
    </div>
  );
};
```

Aşağıdaki örnekte **useRef(value)**, bir  boolean değerini refere etmektedir. 
Bir API çağrıldığında, componentin state'i component'in unmount olup olmadığı kontrol edilerek değiştirilmektedir. Aksi takdirde, component unmount olmuşken state değişimi bir hata ile sonuçlanacaktı.
```javascript
import { useEffect, useState, useRef } from "react";

export const myComponent = deps => { // deps değişkeninin bir dependency array olduğunu varsayalım.
  const isCurrent = useRef(true);
  const [state, setState] = useState({ data: null, loading: true });

  useEffect(() => {
    return () => {
      // called when the component is going to unmount
      isCurrent.current = false;
    };
  }, []);

  useEffect(() => {
    setTimeout(() => {
          if (isCurrent.current) {
            setState({ data: "Fulfilled", loading: false });
          }
        }, 2000);
  }, deps);

  return state;
};
```

Behind the **useRef(value)** explanation, 
```javascript
// step 1
const obj = { name: "Lucas" }
console.log(obj.name)
obj.name = "Lucy"
console.log(obj.name)

// step2
const nameRef = { current: "Lucas" }
console.log(nameRef.current)

// step3
const nameRef = { current: "Lucas" }
const MyComponent = () => {
    console.log(nameRef.current)
}
MyComponent();

// step4
const nameRef = { current: "Lucas" }
const magicStoreOfAllRefs = () => {
    // nameRef: nameRef
    nameRef
}
const useRef = () => {
    return magicStoreOfAllRefs.nameRef;
}
const MyComponent = () => {
    console.log(nameRef.current);
}
MyComponent();

// step5 - magic boilerplate is first three commands.
const nameRef_INVISIBLE = { current: "Lucas" }
const magicStoreOfAllRefs = () => {
    nameRef: nameRef_INVISIBLE
}
const useRef = () => {
    return magicStoreOfAllRefs.nameRef;
}
///////////////////// magic end
const MyComponent = () => {
    const nameRef = useRef("Lucas");
    console.log(nameRef.current);
}
MyComponent();

// step6 - hidden magic boilerplate
const MyComponent = () => {
    const nameRef = useRef("Lucas");
    console.log(nameRef.current);
    nameRef.current = "Lucy";
}
MyComponent(); // Lucas
MyComponent(); // Lucy [simulate re-render]
/* component re-render (simulasyon için burada re-call edildi) olsa bile useRef bir yerde tutulduğu için bir daha initialize edilmiyor, object olarak biryerde (magicStoreOfAllRefs) tutuluyor, ama kendisi re-render'a neden olmuyor. 

Halbuki normal bir javascript'te her seferinde değişken initialize ederdi.
const MyComponent = () => {
    let name = "Lucas"
    console.log(name);
    name = "Lucy";
}
MyComponent(); // Lucas
MyComponent(); // Lucas

*/
```

Bir başka **useRef(value)** kullanımı: bir durum değişkeninin eski değerini tutmak için kullanılır.

```javascript
// step 1 Basit bir counter yaratalım.
import React, { useRef } from "react";

export default function App () { 
  const [counter, setCounter] = useState(0);
  return (
      <div>Count: {counter}</div>
      <button onClick={() => setCounter(counter + 1)}>
        Increment
      </button>
  );
};

// step 2 Counter'ın previous value'sunu useRef ile tutacağız.
import React, { useRef, useRef, useEffect } from "react";

export default function App () { 
  const [counter, setCounter] = useState(0); // #1
  previousCounterRef = useRef(); // #2

  useEffect(() => { // #4
      previousCounterRef.current = counter;
  }, [counter]);

  return ( // #3
      <div>Count: {counter}</div>
      { typeof previousCounterRef.current !== "undefined" && (
          <h2>Previous: {previousCounterRef.current}</h2> // condition içine almazsaydık ilk render işleminde hata verirdi, çünkü useRef olarak bir initial value vermedik.
      )}
      <button onClick={() => 
            setCounter(counter + 1);
            //setCounter(Math.cell( Math.random() * 10 ));
      }>
        Increment
      </button>
  );
};
```