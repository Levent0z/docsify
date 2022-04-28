tsc --init
tsc -b ./src/somefolder


## Get top-level property descriptors of a class instance

```javascript
const obj = new SomeClass();
Object.entries(Object.getOwnPropertyDescriptors(Object.getPrototypeOf(obj)))
```


## Diagnose typing issues
https://drag13.io/posts/custom-typings/index.html
```bash
tsc --traceResolution
```
