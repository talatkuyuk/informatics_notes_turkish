# React Hooks (useState) Notları
Genel olarak, bir react componentin kendi iç state managementi için kullanılmaktadır.

## Projeye dahil etmek
```javascript
import React, { useState } from "react"
import React, { useState, useEffect } from "react"
import { useState } from "react"
```

## useState
useState bir parametre alır ve bir dizi (array) döndürür. 

useState(parametre) vasıtasıyla, takip edilecek durum değişkeninin ilk değeri belirtilir. Bu parametre bir value olabilir, bir object olabilir, bir arrow function olabilir.

Array içeriğini array destruction ile alırız. Array'in İlk elemanı durumdur (*state*), ikinci eleman durumu güncellemek için kullanılacak fonksiyondur (*setState*).

**setState** fonksiyonu component'in re-render olmasına neden olur.

```javascript
const [name, setName] = useState(initialName)
const [value, setValue] = useState(5)
return (
    <div>
        <button onClick={() => setName("New Name")}>Update Name</button>
        <p>{name}</p>
        <button onClick={() => setValue(value + 1)}>Increment Value</button>
        <p>{value}</p>
        <button onClick={() => setValue(v => v + 1)}>Increment Value</button>
        <p>{value}</p>
    </div>
)
```
Burada ```setValue(currentState => newState)``` şeklinde kullanım aynı anda yapılan bir işleme ilişkin bazen ortaya çıkabilecek (işlemin uzun sürmesi gibi bir durumda) side effecte karşı bir önlem sağlar. (Örneğin aynı durum değişkenini güncelleyen iki ayrı buton olması gibi.)

Pahalı bir operasyon varsa ilk değer arrow fonksiyon olarak tanımlanabilir, böylece pahalı operasyonun her bir render işleminde değil de sadece ilk render işleminde yapılması sağlanır:
```javascript
function expensiveInitialState () { 
    someLogic; 
    return initialValue; 
}
const [value, setValue] = useState(() => {expensiveInitialState()})
```

Eğer state içinde bir nesne (object) tutuluyorsa, ve nesnenin sadece bir elemanı güncellenmek isteniyorsa ... operatörü kullanılmalıdır, aksi takdirde diğer nesne elemanlarının durumu kaybolur.
```javascript
const [{count1, count2}, setCount] = useState({count1: 10, count2: 20});
return (
    <div>
        <button 
            onClick={() => 
                setValue(currentState => ({
                    ...currentState,
                    count1: currentState.count1 + 1
                }))
            }
        >Update First Number</button>
        <button 
            onClick={() => 
                setValue(currentState => ({
                    ...currentState,
                    count2: currentState.count2 + 1
                }))
            }
        >Update Second Number</button>
        <button 
            onClick={() => 
                setValue(currentState => ({
                    count1: currentState.count1 + 1,
                    count2: currentState.count2 + 1
                }))
            }
        >Update Both Number</button>
        <p>1.nci sayı: {count1}</p>
        <p>2.nci sayı: {count2}</p>
    </div>
)
```

State içinde örneğin iki elemanlı bir nesne (object) varsa, basitleştirmek için iki ayrı state kullanabiliriz.
```javascript
const [count1, setCount1] = useState(10);
const [count2, setCount2] = useState(20);
return (
    <div>
        <button 
            onClick={() => 
                setCount1(c => c + 1)
            }
        >Update First Number</button>
        <button 
            onClick={() => 
                setCount2(c => c + 1)
            }
        >Update Second Number</button>
        <button 
            onClick={() => 
                setCount1(c => c + 1);
                setCount2(c => c + 1);
            }
        >Update Both Number</button>
        <p>1.nci sayı: {count1}</p>
        <p>2.nci sayı: {count2}</p>
    </div>
)
```

Örneğin bir html form içeriğini state içinde tutmak için aşağıdaki gibi custom bir hook (useForm) yaratabiliriz.
```javascript
import { useState } from "react";

export const useForm = initialValues => {
  const [values, setValues] = useState(initialValues);

  return [
    values,
    e => {
      setValues({
        ...values,
        [e.target.name]: e.target.value
      });
    }
  ];
};
```
Bu custom hook'u şu şekilde kullanabiliriz.
```javascript
import React from "react";
import { useForm } from "./useForm";

const App = () => {
  const [values, handleChange] = useForm({ email: "", password: "" });
  // const [values2, handleChange2] = useForm({ firstName: "", lastName: "" });

  return (
    <div>
      <>
        <input 
          type="text" 
          name="email" 
          value={values.email} 
          onChange={handleChange} />
        <input
          type="password"
          name="password"
          value={values.password}
          onChange={handleChange}
        />
      </>
    </div>
  );
};

export default App;
```