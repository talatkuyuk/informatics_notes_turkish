
```javascript
export const loadState = () => {
    try {
        const serializedState = localStorage.getItem('state');
        if (serializedState === null)
            return undefined;
        return JSON.parse(serializedState);
    } catch (err) {
        return undefined;
    }
}
```

```javascript
export const saveState = (state) => {
    try {
        const serializedState = JSON.stringify(state);
        localStorage.setItem('state', serializedState);
    } catch (err) {
        // ignore write errors.
    }
}
```

```javascript
import throttle from 'lodash/throttle'

const persistedState = loadState();
const store = createStore(
    todoAppReducer,
    persistedState // initial state of store
);
const saveStateFunc = () => {
    saveState({
        todos: store.getState().todos
    })
}
// inner function isn't called more often than the duration miliseconds
store.subscribe( throttle(saveStateFunc, 1000) )
```


```javascript
import { v4 } from 'node-uuid'

// Bir action objesi
export const todo = (text) => ({
    type: 'ADD_TODO',
    id: v4(),
    text // text: text
})
```

```javascript
import { v4 } from 'node-uuid'

// Bir action objesi
export const todo = (text) => ({
    type: 'ADD_TODO',
    id: v4(),
    text // text: text
})
```

## Store Dispatch metoduna Logging Özelliği eklemek
```javascript
const addLoggingToDispatch = (store) => {
  const rawDispatch = store.dispatch;
  return (action) => {
    console.group(action.type);
    console.log('%c prev state', 'color: gray', store.getState());
    console.log('%c action', 'color: blue', action);
    const returnValue = rawDispatch(action);
    console.log('%c next state', 'color: green', store.getState());
    console.groupEnd(action.type);
    return returnValue;
  }
}

const configureStore = () => {
    const persistedState = loadState();
    const store = createStore(todoApp, persistedState);

    if (process.env.NODE_ENV !== 'production') {
      store.dispatch = addLoggingToDispatch(store);
    }
    ...
```

## delay function
```javascript
const delay = (ms) =>
  new Promise(resolve => setTimeout(resolve, ms));

export const fetchTodos = (filter) =>
  delay(500).then(() => { })
```