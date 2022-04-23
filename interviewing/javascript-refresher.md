# JavaScript 

## Primitives

- undefined
- number
- string
- object
- function

## Strings

```JavaScript
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
```

**Notes**
Mind the difference between string's `substr` and `substring`. How to remember: substr & length, substring and endIndexX have the same number of letters. (The last x reminds that the end index is eXclusive)

## Arrays

Constructors:
```javascript
const arr = new Array(?size);
```

On an array, using `for-in` iterates over the indexes, `for-of` iterates over the values.

Note: When an array is initialized with a size, its length is size but all its cells are "empty", i.e. the array has no keys.
```javascript
    new Array(10).map((v, i) => i);  // map lambda is not executed. This is akin to doing for-in. (for-of would still execute 10 times)
    new Array(10).fill(0).map((v, i) => i);  // map lambda is executed 10 times
```


Given:
```javascript
const a = [0, 1, 2, 3, 4, 5]; // Reset before each example
```

| method                                  | returns                                | mutate | usage                             | output on reset a        | a after any mutation     |
| --------------------------------------- | -------------------------------------- | ------ | --------------------------------- | ------------------------ | ------------------------ |
| `push(...items)`                        | new length                             | yes    | a.push(6)                         | 7                        | [0, 1, 2, 3, 4, 5, 6]    |
|                                         |                                        |        | a.push(6, 7)                      | 8                        | [0, 1, 2, 3, 4, 5, 6, 7] |
|                                         |                                        |        | a.push(...[6, 7])                 | 8                        | [0, 1, 2, 3, 4, 5, 6, 7] |
| `pop()`                                 | popped item from the right             | yes    | a.pop()                           | 5                        | [0, 1, 2, 3, 4]          |
| `shift()`                               | dequeued item from the left            | yes    | a.shift()                         | 0                        | [1, 2, 3, 4, 5]          |
| `unshift`                               | new length                             | yes    | a.unshift(6)                      | 7                        | [6, 0, 1, 2, 3, 4, 5]    |
|                                         |                                        |        | a.unshift(6, 7)                   | 8                        | [6, 7, 0, 1, 2, 3, 4, 5] |
|                                         |                                        |        | a.unshift(...[6, 7])              | 8                        | [6, 7, 0, 1, 2, 3, 4, 5] |
| `slice(?start, ?end)`                   | new array                              | no     | a.slice()                         | [0, 1, 2, 3, 4, 5]       |                          |
|                                         |                                        |        | a.slice(1)                        | [1, 2, 3, 4, 5]          |                          |
|                                         |                                        |        | a.slice(1, 1)                     | []                       |                          |
|                                         |                                        |        | a.slice(1, 2)                     | [1]                      |                          |
|                                         |                                        |        | a.slice(1, 2)                     | [1]                      |                          |
|                                         |                                        |        | a.slice(1, -1)                    | [1, 2, 3, 4]             |                          |
| `splice(start, ?deleteCount, ...items)` | new array of deleted items             | yes    | a.splice()                        | []                       | [0, 1, 2, 3, 4, 5]       |
|                                         |                                        |        | a.splice(0)                       | [0, 1, 2, 3, 4, 5]       | []                       |
|                                         |                                        |        | a.splice(1)                       | [1, 2, 3, 4, 5]          | [0]                      |
|                                         |                                        |        | a.splice(1,1)                     | [1]                      | [0, 2, 3, 4, 5]          |
|                                         |                                        |        | a.splice(3, 1, 6, 7)              | [3]                      | [0, 1, 2, 6, 7, 4, 5]    |
| `concat()`                              | new array of concatenated items        | no     | a.concat([6,7])                   | [0, 1, 2, 3, 4, 5, 6 ,7] |                          |
| `reverse()`                             | the same array, reversed               | yes    | a.reverse()                       | a                        | [5, 4, 3, 2, 1, 0]       |
| `sort(?compareFn)`                      | the same array, sorted                 | yes    | a.sort()                          | a                        | [0, 1, 2, 3, 4, 5]       |
|                                         |                                        |        | a.sort((a,b) => a - b))           | a                        | [0, 1, 2, 3, 4, 5]       |
|                                         |                                        |        | a.sort((a,b) => b - a))           | a                        | [5, 4, 3, 2, 1, 0]       |
| `forEach(iteratorFn, ?thisArg)`         | undefined                              | no     | a.forEach((v, i) =>  {}))         |                          |                          |
| `map(iteratorFn, ?thisArg)`             | a new array                            | no     | a.map((v, i) =>  v*2))            | [0, 2, 4, 6, 8, 10]      |                          |
| `filter(predicateFn, ?thisArg)`         | a new subset array                     | no     | a.filter((v, i) =>  v % 2 === 0)  | [0, 2, 4]                |                          |
| `every(predicateFn, ?thisArg)`          | true if pfn=true for all (or empty)    | no     | a.every((v, i) => v < 6)          | true                     |                          |
|                                         |                                        |        | a.every((v, i) => v < 5)          | false                    |                          |
| `some(predicateFn, ?thisArg)`           | false if pfn=false for all ( or empty) | no     | a.some((v, i) => v < 1)           | true                     |                          |
|                                         |                                        |        | a.some((v, i) => v > 5)           | false                    |                          |
| `reduce(aggregatorFn, ?initValue)`      | aggregate value                        | no     | a.reduce((p, c) => p + c, 0)      | 15                       |                          |
| `reduceRight(aggregatorFn, ?initValue)` | aggregate value                        | no     | a.reduceRight((p, c) => p + c, 0) | 15                       |                          |


**Notes**:
- In `slice`, the optional `end` argument, if positive, is exclusive. If negative, it's the count of omitted elements from the right.
- In `splice`, the optional `items`, if provided are inserted at the `start` index, and the items to the right slide further to the right.
- In `sort`, the array is sorted as string comparison by default, unless a compare function is provided, which should return -1, 0, or 1 for smaller, equal and greater than.
- `splice` and `slice` always returns new arrays. `splice(x,1)` removes one element but still returns a single-element array.
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
where iterable is an array of pairs. Each pair is an array of two elements (the kay and the value).


| member                          | returns                                         |
| ------------------------------- | ----------------------------------------------- |
| `size`                          | Number of entries                               |
| `get(key)`                      | the value of the key, or undefined if not found |
| `set(key, value)`               | the mutated map                                 |
| `clear()`                       | undefined                                       |
| `has(value)`                    | true if value exists                            |
| `delete(key)`                   | true if value existed                           |
| `entries()`                     | iterator (not an array)                         |
| `forEach(iteratorFn, ?thisArg)` | undefined                                       |
| `keys()`                        | iterator (not an array)                         |
| `values()`                      | iterator (not an array)                         |

**Notes:**
- The `iteratorFn` takes as arguments **value**, **key**, and **map**. 
- `Array.from(map.entries())` returns an array of arrays, where the nested arrays are pairs: entry[0] is key, entry[1] is value.
- Always use the `get` method to access a `Map`'s elements, not indexing.

## Utility Functions

- Array.isArray()
- Number.isFinite()
- Number.isInteger() - This can't be relied on for a string to be a valid representation of an integer
- Number.isNaN()
- Number.isSafeInteger()
- Number.parseInt(string, ?radix) - The radix defaults to 10, and indicates the base of the number used in string. `parseInt('100', 2) --> 4`
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
```

