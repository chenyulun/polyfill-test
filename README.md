# polyfill-test

## polyfill.io VS core-js3.9.1
Use the link calculated below
```js
 const featuresList = [
  'default',
  'es2015',
  'es2016',
  'es2017',
  'es2018',
  'es2019',
  'es2020',
  'es2021',
  'globalThis',
  'queueMicrotask',
  // 'URL',
  'URL.prototype.toJSON',
  'URLSearchParams',
  // 'DOMTokenList',
  'DOMTokenList.prototype.@@iterator',
  'DOMTokenList.prototype.forEach',
  'DOMTokenList.prototype.replace',
  'NodeList.prototype.@@iterator',
  'NodeList.prototype.forEach',
  'URL.prototype.toJSON',
  'URLSearchParams',
  'Reflect',
  'Reflect.apply',
  'Reflect.construct',
  'Reflect.defineProperty',
  'Reflect.deleteProperty',
  'Reflect.get',
  'Reflect.getOwnPropertyDescriptor',
  'Reflect.getPrototypeOf',
  'Reflect.has',
  'Reflect.isExtensible',
  'Reflect.ownKeys',
  'Reflect.preventExtensions',
  'Reflect.set',
  'Reflect.setPrototypeOf',
  // 'setImmediate',
]
const features = encodeURIComponent(featuresList.join(','))
console.log(`https://polyfill.io/v3/polyfill.min.js?features=${features}`)
// https://polyfill.io/v3/polyfill.min.js?features=default%2Ces2015%2Ces2016%2Ces2017%2Ces2018%2Ces2019%2Ces2020%2Ces2021%2CglobalThis%2CqueueMicrotask%2CURL.prototype.toJSON%2CURLSearchParams%2CDOMTokenList.prototype.%40%40iterator%2CDOMTokenList.prototype.forEach%2CDOMTokenList.prototype.replace%2CNodeList.prototype.%40%40iterator%2CNodeList.prototype.forEach%2CURL.prototype.toJSON%2CURLSearchParams%2CReflect%2CReflect.apply%2CReflect.construct%2CReflect.defineProperty%2CReflect.deleteProperty%2CReflect.get%2CReflect.getOwnPropertyDescriptor%2CReflect.getPrototypeOf%2CReflect.has%2CReflect.isExtensible%2CReflect.ownKeys%2CReflect.preventExtensions%2CReflect.set%2CReflect.setPrototypeOf
```
Core-js compiles the full code `minified.js`

The patch gap in the lower version of the phone is too big

### Test steps
```shell
~ yarn
~ yarn http-server -p 8085 -c-1
```
Choose a lower version of Chrome /41

Open a browser to `http://ip:8085/tests/index.html`

2. Add the core - js - 3.19.1  
open file  `tests/index.html`
```dif
+ <script src='./minified.js'></script>
<script src='./tests.js'></script>
```
You can see it's basically all green

3. add polyfill.io  
`tests/index.html`

```dif
- <script src='./minified.js'></script>
+ <script src="https://polyfill.io/v3/polyfill.min.js?features=default%2Ces2015%2Ces2016%2Ces2017%2Ces2018%2Ces2019%2Ces2020%2Ces2021%2CglobalThis%2CqueueMicrotask%2CURL.prototype.toJSON%2CURLSearchParams%2CDOMTokenList.prototype.%40%40iterator%2CDOMTokenList.prototype.forEach%2CDOMTokenList.prototype.replace%2CNodeList.prototype.%40%40iterator%2CNodeList.prototype.forEach%2CURL.prototype.toJSON%2CURLSearchParams%2CReflect%2CReflect.apply%2CReflect.construct%2CReflect.defineProperty%2CReflect.deleteProperty%2CReflect.get%2CReflect.getOwnPropertyDescriptor%2CReflect.getPrototypeOf%2CReflect.has%2CReflect.isExtensible%2CReflect.ownKeys%2CReflect.preventExtensions%2CReflect.set%2CReflect.setPrototypeOf"></script>
<script src='./tests.js'></script>
```
Ignore esNext， Many polyfills are defective，Especially when it comes to symbols
example
```js
new URL('http://a#б').hash === '#%D0%B1' // chrome95 and core-js:true polyfill.io: false
1 / [1].indexOf(1, -0) > 0 // chrome95 and core-js: true polyfill.io: false
new Int8Array(null) // 
[].at //
Array.prototype[Symbol.unscopables].find //
```