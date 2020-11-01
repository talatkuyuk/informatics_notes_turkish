# React Hooks (useRef) Notları
useRef, javascript kütüphanesi olan React içinde kullanılan yer alan bir hook (fonksiyon)'tur.

Genel olarak, bir Virtual DOM objesini referans etmek, component içinde state'i değiştirmeyecek şekilde bir değişkeni kontrol etmek, durum (state) değişkeninin bir önceki değerini tutmak, bir fonksiyon çağırmak vb. için kullanılmaktadır.

useRef değişkeninin değeri değiştiğinde useState'ten farklı olarak re-render gerçekleşmez. Yani durum değişmez.

## Projeye dahil etmek
```javascript
import React, { useRef } from "react"
import { useRef } from "react"
```

## useRef
+ useRef'in aldığı parametre opsiyoneldir.
+ Eğer useRef bir Virtual DOM objesini refere edecekse paramatre almasına gerek yoktur.
+ Eğer bir değişken veya fonksiyon barındıracaksa bunu parametre olarak alır.

> useRef refere ettiği VirtualDOM objesini veya değer/fonksiyonu döndürür. Bu durum, refere edilen DOM objesinde **ref={somethingRef}** parametresi ile belirtilir.

Aşağıdaki örnekte **useRef()**, bir Virtual DOM objesini refere etmektedir. Butona basıldığında refere edilen DOM objesi etkin (focus) olmakta, arka plan rengi değiştirilmektedir.
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

Aşağıdaki örnekte **useRef(function)**, bir fonksiyonu refere etmektedir. Butona her basıldığında consola ilgili mesaj yazmaktadır.
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

Aşağıdaki örnekte **useRef(value)**, bir  boolean değerini refere etmektedir. Örnekte ikinci useEffect ile bir API çağrılmakta ve sonucu 2 sn sonra geldiği simule edilmektedir. Ama bu arada bu component unmount olabilir (niye?: örneğin bir butona basıldığında bu component ortadan kalkıyor şeklinde bir logic kurulmuş olabilir.). Dolayısıyla componentin state'i, unmount olup olmadığı kontrol edilerek değiştirilmesi gerekmektedir. Aksi takdirde, component unmount olmuşken state değişimi bir hata ile sonuçlanacaktır. İşte bu use case *useRef ve ilk useEffect sayesinde* implement edilmiştir.
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

Aşağıdaki örnekte  bir durum (state) değişkeninin eski değerini tutmak için **useRef(value)**  kullanılmaktadır.
```javascript
// step 1 useState ile basit bir counter yaratalım.
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

// step 2 counter'ın önceki değerini (previous value) useRef ile tutacağız.
import React, { useRef, useRef, useEffect } from "react";

export default function App () { 
  const [counter, setCounter] = useState(0); // #1
  previousCounterRef = useRef(); // #2

  useEffect(() => { 
      previousCounterRef.current = counter; // #4
  }, [counter]);

  return ( // #3
      <div>Count: {counter}</div>
      { typeof previousCounterRef.current !== "undefined" && (
          <h2>Previous: {previousCounterRef.current}</h2> // condition içine almazsaydık ilk render işleminde hata verirdi, çünkü useRef olarak bir initial value vermedik.
      )}
      <button onClick={() => 
            setCounter(counter + 1); // #5
            //setCounter(Math.cell( Math.random() * 10 ));
      }>
        Increment
      </button>
  );
};
```
useRef arkasında nasıl bir mekanizma var, adım adım açıklayalım.
Explaination: Behind the **useRef(value)**
```javascript
// step 1 normal bir javascript objesi
const obj = { name: "Lucas" }
console.log(obj.name)
obj.name = "Lucy"
console.log(obj.name)

// step2 aynı javascript objesini farklı isimlerle yaratalım, benzemeye başladı mı :)
const nameRef = { current: "Lucas" }
console.log(nameRef.current)

// step3 Component içinde gösterelim.
const nameRef = { current: "Lucas" }
const MyComponent = () => {
    console.log(nameRef.current)
}
MyComponent();

// step4 arkada bir store yaratıp yavaş yavaş react'ın mantığına ulaşıyoruz.
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

// step5 - işte: React, useRef değişkenini aslında bir store'da saklıyor.
///////////////////// magic starts.
const nameRef_INVISIBLE = { current: "Lucas" }
const magicStoreOfAllRefs = () => {
    nameRef: nameRef_INVISIBLE
}
const useRef = () => {
    return magicStoreOfAllRefs.nameRef;
}
///////////////////// magic ends. aşağısı ise useRef'in görünen kısmı
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
/* component re-render (simulasyon için burada re-call edildi) olsa bile useRef bir yerde tutulduğu için bir daha initialize edilmiyor, object olarak bir yerde (magicStoreOfAllRefs) tutuluyor, ama kendisi re-render'a neden olmuyor. 

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