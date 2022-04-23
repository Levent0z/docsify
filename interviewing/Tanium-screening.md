# Tanium

Tech-Screened on 4/24/2018 via [CodeInterview.io](https://codeinterview.io/).

## Tech-Screen Interview Question

Implement the `parseRange` function which takes a comma-separated series of single years, or year ranges and returns an array of finite years which correspond to the given input.

Constraints:
- Valid years are 1999 to current year
- Years must not repeat
- Sorted

<details>
<summary>Starting Point</summary>
This was provided.

```javascript
// Installed npm packages: jquery underscore request express
// jade shelljs passport http sys lodash async mocha chai sinon
// sinon-chai moment connect validator restify ejs ws co when
// helmet wrench brain mustache should backbone forever debug jsdom

// Implement the parseRange function which takes a comma separated
// series of single years, or year ranges and returns an array of finite years
// which correspond to the given input.
// Constraints:
// Valid years are 1999 to current year
// Years must not repeat
// Sorted
const assert = require('assert');
const _ = require('lodash');
// _.includes(collection, value, [fromIndex=0])
// _.includes('abcd', 'bc');
// => true
```
</details>

<details>
<summary>Define test cases and test method</summary>

It is very important to understand the kind of input before writing code. Depending on the interviewer's answers, your solution might get more or less complicated. 

*Note*: Original test cases from 2018 have been augmented with new ones in 2022, and any test cases that assumed maxYear = 2018 were fixed (for 2022).

```javascript
const testCases = [
  // All Invalids
  [undefined, []],
  ['', []],
  ['. ', []],
  ['   ,  ', []],
  ['1998', []],
  ['2023', []],
  ['-1999', []],
  ['1999.5', []],
  ['NaN', []],
  ['xyz', []],
  ['2021-', []],
  ['2017 - ', []],
  [' - 2017', []],
  ['2015 - 2017 - ', []],
  [' - 2015 - 2017', []],
  ['2017 - 2015', []],
  ['1999 - 3000', []],
  ['1998, 2024', []],
  ['1998 - 2012', []],
  ['xyz - 2012', []],
  
  // Valids
  ['1999', [1999]],
  ['2017', [2017]],
  ['2015 - 2015', [2015]],
  ['2015, 2014, 2010', [2010, 2014, 2015]],
  ['2002-2005, 2002-2005, 2002 - 2005', [2002, 2003, 2004, 2005]],
  ['1999-2003', [1999, 2000, 2001, 2002, 2003]],
  ['1999, 2002-2005, 2007', [1999, 2002, 2003, 2004, 2005, 2007]],
  
  // Mixed inputs
  ['1998, 2020', [2020]],
  ['1999 , 2000,    , 2008', [1999, 2000, 2008]],
  ['1999, 3000', [1999]],
  ['1980-2003,2000 -2002, 0,2019 - 2023, 2022, 2019-2018, 2017-2017', [2000,2001,2002,2017,2022]],  
];

function test(testFunc) {
    for (let i = 0; i < testCases.length; i += 1 ) {
      const tc = testCases[i];
      const input = tc[0];
      const expected = tc[1];
      const actual = testFunc(input);
      
      const passed = Array.isArray(actual) && expected.length === actual.length && expected.every((e, i) => actual.indexOf(e) === i);
      if (passed) {
        console.log(`${i}: Passed.`);  
      } else {
        console.error(`${i}: Failed, returned ${JSON.stringify(actual)}`);  
      }
    }
}
```
</details>


<details>
<summary>Implementation from 2018</summary>
This was the actual solution I came up with during the interview.

```javascript
'use strict';

function filterInt(value) {
    // Based on https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt

    if (/^(\-|\+)?([0-9]+|Infinity)$/.test(value)) {
        return Number(value);
    }
    return NaN;
}

function parseRange(rangeStr) {
    if (!rangeStr) {
        return [];
    }

    let splitDash = (text) => text.split('-').map(i => i.trim());
    let splitComma = (text) => text.split(',').filter(i => i && i.trim() !== '').map(i => i.trim());

    let tokens = splitComma(rangeStr);

    let results = new Set();

    const minYear = 1999;
    let maxYear = (new Date()).getFullYear();
    let checkRange = (value) => (value >= minYear && value <= maxYear);

    tokens.forEach(t => {

        // Handle ranges indicated by the presence of a dash
        if (t.indexOf('-') >= 0) {
            let range = splitDash(t);
            if (range.length !== 2) {
                return;
            }

            let first = filterInt(range[0]);
            let second = filterInt(range[1]);


            if (!checkRange(first) || !checkRange(second)) {
                // We need the range to be valid
                return;
            }

            for (let i = first; i <= second; i++) {
                results.add(i);
            }

        } else {

            let value = filterInt(t);

            if (checkRange(value)) {
                results.add(value);
            }
        }
    });

    return Array.from(results).sort();
}

test(parseRange);
```
</details>

<details>
<summary>Implementation from 2022</summary>
I redid it for practice.

```javascript
'use strict';

const minYear = 1999;
const maxYear = new Date().getFullYear();

function isValid(text) {
  const num = Number(text);
  return text === '' || !Number.isNaN(num) && Number.parseInt(text) === num;
}

function parseRange2(csvText) {
    const minYear = 1999;    
    const maxYear = new Date().getFullYear();
    
  if (!csvText) {
    return [];
  }
  const set = new Set();
  
  csvText.split(',').forEach(e => {    
    const pair = e.split('-').map(i => i.trim());
    
    if (pair.length > 2 || pair.some(i => !isValid(i))) {
      return;
    }
    let start = pair[0];
    let end = pair.length === 2 ? pair[1] : start;
    
    if (!isValid(start) || !isValid(end)) {
      return;
    }
    start = Number(start);
    end = Number(end);
    if (start > end || start < minYear || end > maxYear) {
      return;
    }
    
    for (let year = start; year <= end; year += 1) {
      set.add(year);
    }     
  });
  
  return Array.from(set).sort();
}

test(parseRange2);
```
</details>

<br>

> Code available on [repl.it](https://replit.com/@leventoz/InputParseForYearRanges#index.js).