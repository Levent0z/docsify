# JavaScript 


## Arrays

Given:
```JavaScript
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
- The **iteratorFn** takes as arguments **value**, **index**, and **array**. In `map`, the return value of the iteratorFn is pushed into the returned array. 
- The **predicateFn** takes as arguments **value**, **index**, and **array**. It needs to return a truthy value.
- The **aggregatorFn** takes as arguments **aggregate**, **current**, **index**, and **array**. The initial value of the aggregate is the second argument to reduce.
- `every` checks for compliance. Can be used as an alternative to `forEach`: return false in the predicate to end the iteration (similar to breaking in a for loop).
- `some` checks for existence. Can be used as an alternative to `forEach`: return true in the predicate to end the iteration.

## Sets
Stores unique values of any type. You can iterate through it in insertion order.

Constructor:
```
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
```
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
- The iteratorFn takes as arguments **value**, **key**, and **map**. 


## Utility Functions

- Array.isArray()
- Number.isFinite()
- Number.isInteger()
- Number.isNaN()
- Number.isSafeInteger()
- Number.parseInt()
- Number.parseFloat()
- Object.hasOwnProperty()


## Things to know

```JavaScript
NaN === NaN // false. However, if NaN was a key in a Set/Map, there could only be one.

Infinity === Infinity // true
Infinity === Number.POSITIVE_INFINITY // true
Infinity === Number.NEGATIVE_INFINITY // false

const a = new Array(10);
a.length === 10 // true
a[0] === undefined // true, in fact all entries are undefined. So be careful preinitializing arrays if using lengths
```