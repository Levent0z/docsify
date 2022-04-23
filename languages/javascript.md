# JavaScript

## Overview

- Weakly-typed, interpreted, JIT-ted language
- Used in browsers, Node (V8), Webviews, JsCore

## Comments
- Single line, using `//`
- Multi line, using `/*` and `*/`

## Data Types

Primitive types: `undefined`, `string`, `number`, `boolean`, `object`
 
### Booleans

`true` and `false`.

- The following are "falsy": `undefined`, `null`, `''`, `""`, `0`
- The following are "truthy": `{}`, `[]`, numbers

### Numbers

Numbers are always doubles. No built-in integer types.

Watch out for decimal arithmetic:
```javascript
    0.2 + 0.7 == 0.9                      // false
    0.2 + 0.7 == 0.8999999999999999       // true
```

Notations
- Decimal
- Octal, prefixed with `0`, but only if valid octal number
- Hexadecimal, prefixed with `0x`

### Strings

- Inside pair of single-quotes, double-quotes or backticks
- Empty string: `''`, `""`, or ``.
- Immutable
- String interpolation syntax only inside backtick.
- No string builder
  
```javascript
    'String' + 'concatenation'
    `String interpolation ${variableOrExpression}`
```

### Objects
- Objects are dictionaries (key-value pairs)
- Empty object: `{}`
- No native method to get memory size of the object.

### Arrays
- Arrays are objects.
- Empty array: `[]`
- Indexes are 0-based.

### Type checking

- Check primitive types using `typeof`.
- Check `new`'ed objected using `instanceof`.

```javascript
    typeof undefined === 'undefined'      // true
    typeof null === 'object'              // true
    typeof [] === 'object'                // true
    [] instanceof Array                   // true
    Array.isArray([]) === true            // true
```



## Variable declaration

`var`, `let`, `const`

## Comparators

`==`, `===`, `<`, `>`, `<=`, `>=`, `!=`, `!==`

## Logical operators

`&&`, `||`

## Unary Operators

`-`, `!`, `~`

## Binary operators

`+=`, `-=`, `*=`, `/=`, `&&=`, `||=`

## Flow Control

### Ternary operator using `?` and `:`:
```javascript
const result = expression ? resultIfTrue : resultIfFalse;
```

### If statement
```javascript
if (expression1 ) {
    // body if expression1 is true
} else if (expression2) {
    // body if expression1 is false and expression 2 is true
} else {
    // body if neither expression are true
}
```

### Switch Statement
```javascript
switch(expression) {
    case 'text': // hard-coded string
        // body if match
        break;
    case 0: // hard-coded number 
        // body if match
        break;
    default:
        // body if no match
        break;
}
```

### Loops
```javascript
for (const variable of iterable) {
    // Iteration for each item in the iterable
}

for (const variable in object) {
    // Iteration for each key in the dictionary
}

for (let variable=initialValue; expression; variable += 1) {
    // Iteration so lon as expression is true
}

while (expression) {
    // Iteration so long as expression is true
}

do {
    // Execute at least once, repeat if expression is true
} while (expression);
```


## Functions

```javascript
function func0() {
}
function func1(arg1) {
}
function func2(arg1, ...argRest) {
}

const lambda0 = () => { };
const lambda1 = (arg1) => { };
const lambda2 = (arg2, ...argRest) => { };
```

### return

- Return values with the `return` statement. The returned value **must** be on the same line.
- If no `return` statement, the function returns `undefined`.

### this

- Inside a `function` definition, `this` is the object that calls the function, unless bound.
- Inside a lambda, `this` retains its value from the closure.

### bind()
- The `bind` method of a function returns another function, whose `this` is bound to the specified argument.
- Class methods should be bound before passed outside the class as a function. The method should be bound to the class instance.
- Binding cannot be undone.

### apply()

Use `apply` method of a function to call it with a specified `this` and an array of arguments.

### call()

Use `call` methods of a function to call it with a specified `this` and individual arguments.

## Exceptions
```javascript
    try {
        throw new Error('message');
    } catch (err) {
        // Body if exception
    } finally {
        // Body that will always be executed
    }
```


# Operations
## Strings

```javascript
const str = 'Some Text';

// True statements follow:
str.length === 9    
str.toUpperCase() === 'SOME TEXT'
str.toLowerCase() === 'some text'
str[0] === 'S'
str.indexOf('Z') === -1
str.indexOf('e') === 3
str.lastIndexOf('e') === 6
str.substr(1, 2) === 'om'           // (from, ?length)
str.substring(1, 2) === 'o'         // (start, ?end). Similar to "slice"
str.substr(1) === str.substring(1)  // Equivalent without second arg
str.search(/e.+e/) === 3            
str.padStart(12, '-') === '---Some Text'
str.padEnd(12, '-') === 'Some Text---'
str.split(' ').length === 2         // Returns ['Some', 'Text']
str.charAt(2) === 'o'               // charAt() returns empty string if not found
str[2] === 'o'                      // Indexing returns undefined if not found
str.charCodeAt(0) === 83            // ASCII code of 'S'
'S' === '\u0053'                    // Unicode-escape notation using hexadecimals
```

## Arrays

```javascript
const arr = [];
arr.length === 0        // True
arr === []              // False,  Arrays are object, and these are two different empty arrays
```

### Mutating methods
- fill
- push                           // adds element at end
- shift                          // adds element in the beginning
- pop                            // removes element from end
- unshift                        // removes element from the beginning
- sort                           // sorts the elements
- splice(start, ?deleteCount)    // deletes the range of elements from the array

### Non-mutating methods (returns new array)
- concat(secondArray)            // Adds elements of second array to first array
- slice(?start, ?end)            // returns a new array containing the elements in the range
- filter(predicate)
- map(lambda)
