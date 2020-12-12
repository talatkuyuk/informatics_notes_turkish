# Javascript Modules in ES6 (aka ES2015)

### Importing Modules
```javascript
import package from 'module-name'

import * from 'mymodule'
import React from 'react'
import { React, Component } from 'react'
import React as MyLibrary from 'react'
```

### Exporting Modules
```javascript
export var number = 2
export function bar() { /* ... */ }

```

### Default Exports
This creates one default export. 
```javascript
// uppercase.js
export default str => str.toUpperCase()

import toUpperCase from 'https://flavio.me/uppercase.js' // valid
import toUpperCase from './uppercase.js' // valid
import toUpperCase from '../uppercase.js' // valid
import { toUpperCase } from '/uppercase.js' // valid
import { toUpperCase } from '../uppercase.js' // valid
import { toUpperCase } from 'uppercase.js' // X invalid
import { toUpperCase } from 'utils/uppercase.js' // X invalid
toUpperCase('test') //'TEST'
```

### Multi Exports
In a file however we can export more than one.
```javascript
const a = 1
const b = 2
const c = 3
export { a, b, c }

import * from 'module'
import { a } from 'module'
import { a, b } from 'module'
import { a, b as two } from 'module'
```

###  An HTML page can add a module 
```html
<script type="module" src="index.js"></script>

<!-- What about browsers that do not support modules? -->
<script type="module" src="module.js"></script>
<script nomodule src="fallback.js"></script>
```