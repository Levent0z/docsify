# JavaScript 

## Primitives

- undefined
- number
- string
- object
- function

## Hoisting and variable types
- `var` variables are function-scoped, can be used before they are declared.
- `let` variables are block-scoped, can be declared anywhere in the block but can't be used before they are initialized.
- `const` variables are block-scoped, must be declared and initialized at the same time, anywhere in the block.

## Numbers

```javascript
(16).toString(2)        // '10000'
(16).toString(16)       // '10'

parseInt('10000', 2)    // 16
parseInt('10', 16)      // 16

// Bitwise negation operator can be surprising (uses 32-bit signed ints internally), but results are 64-bit doubles
~5                      // -6
(-6).toString(2)        // '-110'
(~5).toString(2)        // '-110'

// Use the "zero-fill right-shift" operator to convert to unsigned 32-bits
-1 >>> 0                // 4294967295 (max uint32)
~5 >>> 0                // 4294967290
-6 >>> 0                // 4294967290

(-6 >>> 0).toString(2)  // '11111111111111111111111111111010'
(~5 >>> 0).toString(2)  // '11111111111111111111111111111010'
```

Note: Can't calculate max uin64 accurately, because its value (18446744073709551615) is greater than `Number.MAX_SAFE_INTEGER` (9007199254740991).

## Strings

```javascript
const a = '0123456';
a.substr(0, 0)    // ''    Second argument is length
a.substring(0, 0) // ''    Second argument is end index (not inclusive)

a.substr(0, 2)    // '01'   Second argument is length
a.substring(0, 2) // '01'   Second argument is end index (not inclusive)

a.substr(1, 2)    // '12'   Second argument is length
a.substring(1, 2) // '1'    Second argument is end index (not inclusive)

a.substr(1)       // '123456'
a.substring(1)    // '123456'

'a'.charcodeAt(0)           // 97
String.fromCharCode(97)     // 'a'  

'a,b ,c, d , e f'.split(/\s*,\s*/);    // ['a', 'b', 'c', 'd', 'e f']
```

**Notes**
- Mind the difference between functions `substr` and `substring`. How to remember: substr & length, substring and endIndexX have the same number of letters. (The last x reminds that the end index is eXclusive)
- If the second argument is omitted from `substr` or `subtring`, the implied intent is the rest of the characters.

## Objects

Defining a getter:
```javascript
const obj = {};
Object.defineProperty(obj, 'pi', { value: Math.PI, writeable: false});
console.log(obj.pi);
```

## Arrays

Constructor:
```javascript
const arr = new Array(?size);
```

On an array, using `for-in` iterates over the keys (indexes + names keys if any), `for-of` iterates over indexed values (only).

Note: When an array is initialized with a size, its length is size but all its cells are "empty", i.e. the array has no keys.
```javascript
new Array(10).map((v, i) => i);  // map lambda is not executed. This is akin to doing for-in. (for-of would still execute 10 times)
new Array(10).fill(0).map((v, i) => i);  // map lambda is executed 10 times
```


Given:
```javascript
const a = [0, 1, 2, 3, 4, 5]; // Reset before each example
```

| method                                  | returns                                     | mutate | usage                             | output on reset a        | a after any mutation     |
| --------------------------------------- | ------------------------------------------- | ------ | --------------------------------- | ------------------------ | ------------------------ |
| `push(...items)`                        | new length                                  | yes    | a.push(6)                         | 7                        | [0, 1, 2, 3, 4, 5, 6]    |
|                                         |                                             |        | a.push(6, 7)                      | 8                        | [0, 1, 2, 3, 4, 5, 6, 7] |
|                                         |                                             |        | a.push(...[6, 7])                 | 8                        | [0, 1, 2, 3, 4, 5, 6, 7] |
| `pop()`                                 | popped item from the right                  | yes    | a.pop()                           | 5                        | [0, 1, 2, 3, 4]          |
| `shift()`                               | dequeued item from the left                 | yes    | a.shift()                         | 0                        | [1, 2, 3, 4, 5]          |
| `unshift`                               | new length                                  | yes    | a.unshift(6)                      | 7                        | [6, 0, 1, 2, 3, 4, 5]    |
|                                         |                                             |        | a.unshift(6, 7)                   | 8                        | [6, 7, 0, 1, 2, 3, 4, 5] |
|                                         |                                             |        | a.unshift(...[6, 7])              | 8                        | [6, 7, 0, 1, 2, 3, 4, 5] |
| `slice(?start, ?end)`                   | new array                                   | no     | a.slice()                         | [0, 1, 2, 3, 4, 5]       |                          |
|                                         |                                             |        | a.slice(1)                        | [1, 2, 3, 4, 5]          |                          |
|                                         |                                             |        | a.slice(1, 1)                     | []                       |                          |
|                                         |                                             |        | a.slice(1, 2)                     | [1]                      |                          |
|                                         |                                             |        | a.slice(1, -1)                    | [1, 2, 3, 4]             |                          |
| `splice(start, ?deleteCount, ...items)` | new array of deleted items                  | yes    | a.splice()                        | []                       | [0, 1, 2, 3, 4, 5]       |
|                                         |                                             |        | a.splice(0)                       | [0, 1, 2, 3, 4, 5]       | []                       |
|                                         |                                             |        | a.splice(1)                       | [1, 2, 3, 4, 5]          | [0]                      |
|                                         |                                             |        | a.splice(1,1)                     | [1]                      | [0, 2, 3, 4, 5]          |
|                                         |                                             |        | a.splice(3, 1, 6, 7)              | [3]                      | [0, 1, 2, 6, 7, 4, 5]    |
| `concat()`                              | new array of concatenated items             | no     | a.concat([6,7])                   | [0, 1, 2, 3, 4, 5, 6 ,7] |                          |
| `reverse()`                             | the same array, reversed                    | yes    | a.reverse()                       | a                        | [5, 4, 3, 2, 1, 0]       |
| `sort(?compareFn)`                      | the same array, sorted                      | yes    | a.sort()                          | a                        | [0, 1, 2, 3, 4, 5]       |
|                                         |                                             |        | a.sort((a,b) => a - b))           | a                        | [0, 1, 2, 3, 4, 5]       |
|                                         |                                             |        | a.sort((a,b) => b - a))           | a                        | [5, 4, 3, 2, 1, 0]       |
| `forEach(iteratorFn, ?thisArg)`         | undefined                                   | no     | a.forEach((v, i) =>  {}))         |                          |                          |
| `map(iteratorFn, ?thisArg)`             | a new array                                 | no     | a.map((v, i) =>  v*2))            | [0, 2, 4, 6, 8, 10]      |                          |
| `filter(predicateFn, ?thisArg)`         | a new subset array                          | no     | a.filter((v, i) =>  v % 2 === 0)  | [0, 2, 4]                |                          |
| `every(predicateFn, ?thisArg)`          | true if pfn=true for all (or empty)         | no     | a.every((v, i) => v < 6)          | true                     |                          |
|                                         |                                             |        | a.every((v, i) => v < 5)          | false                    |                          |
| `some(predicateFn, ?thisArg)`           | false if pfn=false for all ( or empty)      | no     | a.some((v, i) => v < 1)           | true                     |                          |
|                                         |                                             |        | a.some((v, i) => v > 5)           | false                    |                          |
| `reduce(aggregatorFn, ?initValue)`      | aggregate value                             | no     | a.reduce((p, c) => p + c, 0)      | 15                       |                          |
| `reduceRight(aggregatorFn, ?initValue)` | aggregate value                             | no     | a.reduceRight((p, c) => p + c, 0) | 15                       |                          |
| `flat(?depth)`                          | new array, flattened recursively upto depth | no     | a.flat()                          | [0, 1, 2, 3, 4, 5]       |                          |
|                                         |                                             | no     | [1, [2, 3]].flat()                | [1, 2, 3]                |                          |


**Notes**:
- You can use `slice` without any arguments to shallow-clone an array.
- In `slice`, the optional `end` argument, if positive, is exclusive. If negative, it's the count of omitted elements from the right.
- In `splice`, the optional `items`, if provided are inserted at the `start` index, and the items to the right slide further to the right.
- In `sort`, the array is sorted as string comparison by default, unless a compare function is provided, which should return -1, 0, or 1 for smaller, equal and greater than.
- `splice` and `slice` always return new arrays. `splice(x,1)` removes one element but still returns a single-element array.
- If the second argument is omitted from `splice` or `slice`, the implied intent is the rest of the items.
- The **iteratorFn** takes as arguments **value**, **index**, and **array**. In `map`, the return value of the iteratorFn is pushed into the returned array. 
- The **predicateFn** takes as arguments **value**, **index**, and **array**. It needs to return a truthy value.
- The **aggregatorFn** takes as arguments **aggregate**, **current**, **index**, and **array**. The initial value of the aggregate is the second argument to reduce.
- `every` checks for compliance. Can be used as an alternative to `forEach`: return false in the predicate to end the iteration (similar to breaking in a for loop).
- `some` checks for existence. Can be used as an alternative to `forEach`: return true in the predicate to end the iteration.

## Sets
Stores unique values of any type. You can iterate through it in insertion order.

Constructor:
```javascript
new Set(?iterable) 
```
where iterable is an array of values.


| member                          | returns                    |
| ------------------------------- | -------------------------- |
| `size`                          | Number of entries          |
| `add(value)`                    | the mutated set            |
| `clear()`                       | undefined                  |
| `has(value)`                    | true if value exists       |
| `delete(value)`                 | true if value existed      |
| `entries()`                     | an iterable (not an array) |
| `forEach(iteratorFn, ?thisArg)` | undefined                  |
| `keys()`                        | SetIterator (not an array) |
| `values()`                      | SetIterator (not an array) |

**Notes:**
- The iteratorFn takes as arguments **value**, **key**, and **set**. Value and key are the same.


## Maps
Stores key-value pairs and remembers the original insertion order of the keys. Any value (both objects and primitive values) may be used as either a key or a value.

Constructor
```javascript
new Map(?iterable)
```
where iterable is an array of pairs. Each pair is an array of two elements (the key and the value).


| member                          | returns                                         |
| ------------------------------- | ----------------------------------------------- |
| `size`                          | Number of entries                               |
| `get(key)`                      | the value of the key, or undefined if not found |
| `set(key, value)`               | the mutated map                                 |
| `clear()`                       | undefined                                       |
| `has(key)`                      | true if key exists                              |
| `delete(key)`                   | true if key existed                             |
| `entries()`                     | iterator (not an array)                         |
| `forEach(iteratorFn, ?thisArg)` | undefined                                       |
| `keys()`                        | iterator (not an array)                         |
| `values()`                      | iterator (not an array)                         |

**Notes:**
- The `iteratorFn` takes as arguments **value**, **key**, and **map**. 
- `Array.from(map.entries())` returns an array of arrays, where the nested arrays are pairs: entry[0] is key, entry[1] is value.
- Always use the `get` method to access a `Map`'s elements, not indexing.

## Converting a POJO into a map
```javascript
const map = new Map();
for (const key in pojo) { 
    map.set(key, pojo[key]); 
}
```

## Sorting a map
```javascript
const sortedOnKeys = new Map(Array.from(unsorted.entries()).sort((a, b) => a[0] < b[0] ? -1 : a[0] > b[0] ? 1 : 0));
const sortedOnValues = new Map(Array.from(unsorted.entries()).sort((a, b) => a[1] < b[1] ? -1 : a[1] > b[1] ? 1 : 0));
```

## Utility Functions

- Array.isArray()
- Number.isFinite()
- Number.isInteger() - This can't be relied on for a string to be a valid representation of an integer
- Number.isNaN()
- Number.isSafeInteger()
- Number.parseInt(string, ?radix) - The radix defaults to 10 (unless the string starts with '0x' or '0X' in which case it defaults to 16), and indicates the base of the number used in string. `parseInt('100', 2) --> 4`
- Number.parseFloat(string)
- hasOwnProperty()
- Object.keys()     - Unlike Set/Map's keys method, this returns an actual array, not an iterator.
- Object.entries()  - Unlike Set/Map's entries method, this returns an actual array (of pairs), not an iterator.


## Things to know

```javascript
NaN === NaN // false. However, if NaN was a key in a Set/Map, there could only be one.

Infinity === Infinity // true
Infinity === Number.POSITIVE_INFINITY // true
Infinity === Number.NEGATIVE_INFINITY // false

const a = new Array(10);
a.length === 10 // true
a[0] === undefined // true, in fact all entries are undefined. So be careful preinitializing arrays if using lengths

parseInt === Number.parseInt // true
parseFloat === Number.parseFloat // true
```

## Object Prototypes

Every object in JavaScript has a built-in property, which is called its prototype. The prototype is itself an object, so the prototype will have its own prototype, making what's called a **prototype chain**. The chain ends when we reach a prototype that has `null` for its own prototype.

```javascript
class C {
    f() {
        return true;
    }
}
typeof C === 'function' // true
let c1 = new C();
typeof c1 === 'object' // true

let c1p = Object.getPrototypeOf(c1);    // This is the standard way, not __proto__
typeof c1p === 'object' // true
c1p.constructor === C   // true

let c1pp = Object.getPrototypeOf(c1p);  // Still an object
Object.getPrototypeOf(c1pp)) === null // true
```

When you try to access a property of an object: if the property can't be found in the object itself, the prototype is searched for the property. If the property still can't be found, then the prototype's prototype is searched, and so on until either the property is found, or the end of the chain is reached, in which case undefined is returned.

In JavaScript, all `function`s have a property named `prototype`. When you call a function as a constructor, this property is set as the prototype of the newly constructed object (by convention, in the property named `__proto__`).

```javascript
const personPrototype = {
  greet() {
    console.log(`hello, my name is ${this.name}!`);
  }
}

function Person(name) {
  this.name = name;
}

Person.prototype = personPrototype;
Person.prototype.constructor = Person;

new Person('Levent').greet(); // hello, my name is Levent!
```


## Promises

```javascript
const p = new Promise((resolve, reject) => {
    someFuncThatTakesCallback((value, error) => {
       if (error) {
           reject(error);
       } else {
           resolve(value);
       }
    });
});

p.then(value => {

}).catch(error => {

}).finally(() => {

});

// Alternative to the above:
try {
    // Note: async keyword is required if used in a function
    const value = await p;
} catch (error) {

} finally {

}
```

| Promise method | description                                                                       |
| -------------- | --------------------------------------------------------------------------------- |
| `all`          | resolves if all promises in the iterable resolve. Rejects as soon as one rejects  |
| `allSettled`   | waits for all promises in the iterable to resolve or reject                       |
| `any`          | resolves as soon as one promise in the iterable resolves. Rejects if none resolve |
| `race`         | resolves or rejects as soon as any of the promises settles                        |