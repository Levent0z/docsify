# How to use Jest with TypeScript

This blog shows you step-by-step how to set up a TypeScript project from scratch with Jest enabled for unit-testing. The end-result can be seen at this [Git repo](https://github.com/Levent0z/jest-and-typescript).

## STEP 1: Initialize Node project

```sh
$ npm init
```

This will create a package.json file based on your inputs.

### `package.json`: (Example)

```JSON
{
  "name": "jest-and-typescript",
  "version": "1.0.0",
  "description": "A scaffolding that shows TypeScript working with Jest",
  "main": "index.ts",
  "scripts": {
    "test": "jest"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/levent0z/jest-and-typescript.git"
  },
  "keywords": [
    "Jest",
    "TypeScript",
    "ts-jest"
  ],
  "author": "Levent Oz",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/levent0z/jest-and-typescript/issues"
  },
  "homepage": "https://github.com/levent0z/jest-and-typescript#readme"
}
```

## STEP 2: Install Development Time Dependencies

```bash
$ npm i typescript --save-dev
$ npm i jest --save-dev
$ npm i @types/jest --save-dev      # Type definitions for Jest
$ npm i rimraf --save-dev           # Cross-platform recursive folder remover "rm -rf"
```

After this, the following lines will have been added to `devDependencies` section in package.json. Your versions will most likely be different.

```JSON
  "devDependencies": {
    "@types/jest": "^26.0.14",
    "jest": "^26.4.2",
    "rimraf": "^3.0.2",
    "typescript": "^4.0.3"
  }
```

## STEP 3 - Initialize a TypeScript project:

```sh
$ npx tsc --init
```

If you have TypeScript installed globally, you can omit the `npx` in the above command line.

This will generate a tsconfig.json file. Make a backup of this file in case you want to refer to the commented-out lines later. For brevity, I've removed those lines.

### `tsconfig.json`:

```JSON
{
  "compilerOptions": {
    "target": "es5",                          /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019' or 'ESNEXT'. */
    "module": "commonjs",                     /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext'. */
    "strict": true,                           /* Enable all strict type-checking options. */
    "esModuleInterop": true,                  /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
    "skipLibCheck": true,                     /* Skip type checking of declaration files. */
    "forceConsistentCasingInFileNames": true  /* Disallow inconsistently-cased references to the same file. */
  }
}
```

## Step 4 - Edit tsconfig.json

Make modifications so that the file now looks like the following:

```JSON
{
    "compilerOptions": {
        "target": "ES2015",                           /* Modified */
        "module": "ES2020",                           /* Modified */
        "strict": true,
        "esModuleInterop": true,
        "skipLibCheck": true,
        "forceConsistentCasingInFileNames": true,     /* Edited */
        "moduleResolution": "node",                   /* Added */
        "outDir": "dist",                             /* Added */
    },                                                /* Added */
    "exclude": [                                      /* Edited */
        "node_modules",                               /* Added */
        "**/__tests__"                                /* Added */
    ]                                                 /* Added */
}
```

## STEP 5 - Edit package.json

Add the missing lines into `scripts` section of package.json:

```JSON
  "scripts": {
    "clean": "rimraf dist && jest --clearCache",
    "build": "tsc --build",
    "build:clean": "npm run clean && tsc --build",
    "test": "jest"
  }
```

## STEP 6 - Add a simple TypeScript class

```sh
$ mkdir src
$ touch src/index.ts
```

Copy the following text into index.ts:

### `index.ts`

```TypeScript
export class Main {
    hello(name: string): string {
        return `Hello ${name}!`;
    }
}
```

Make sure it builds:

```sh
$ npm run build # Creates a dist folder and transpiles index.ts into index.js
```

## Step 7 - Add a test

```sh
$ mkdir src/__tests__
$ touch src/__tests__/index.test.js # Using regular JavaScript for tests
```

Copy the following text into index.test.js:

### `index.test.js`

```javascript
import { Main } from '../index';

describe('index', () => {
    it('Responds correctly', () => {
        let main;

        expect(() => { main = new Main(); }).not.toThrow();
        expect(main.hello('world')).toBe('Hello world!');
        expect(main.hello('jest')).toBe('Hello jest!');
    });
});
```

Now run the test:

```sh
$ npm run test
```

At this point, Jest will fail as follows:

```
 FAIL  src/__tests__/index.test.js
  ● Test suite failed to run

    Jest encountered an unexpected token

    ...

    Details:

    /Users/loz/github/levent0z/jest-and-typescript/src/__tests__/index.test.js:1
    import { Main } from '../index';
           ^

    SyntaxError: Unexpected token {
```

This is because Jest currently doesn't understand TypeScript. We need to use a transformer for this purpose. There are several transformers available, such as one from Babel, but in this blog post, we're going to use [TS-Jest](https://github.com/kulshekhar/ts-jest/blob/master/README.md).

## STEP 8 - Install TS-Jest

```sh
$ npm i ts-jest --save-dev
```

This adds the line `"ts-jest": "^26.4.1",` to `devDependencies` in package.json.

## STEP 9 - Add Jest Configuration

```sh
$ mkdir scripts
$ touch scripts/jest.config.js
```

Copy the following into jest.config.js:

### `jest.config.js`

```javascript
module.exports = {
    testMatch: ['<rootDir>/src/**/*.(spec|test).(ts|js)'],
    rootDir: '..',
    transform: {
        '^.+\\.(t|j)s$': 'ts-jest'
    },
    globals: {
        'ts-jest': {
            tsConfig: '<rootDir>/tsconfig.test.json'
        }
    }
};
```

Use this configuration in the `test` script in `scripts` in package.json:

```
"test": "jest --config ./scripts/jest.config.js"
```

## STEP 10 - Add TypeScript configuration for test

Our tsconfig.json file doesn't have the configuration that ts-jest needs. Without affecting our production tsconfig.json, we can extend/override settings in a separate file that we will call tsconfig.test.json.

```sh
$ touch tsconfig.test.json
```

Copy the following into tsconfig.test.json:

### `tsconfig.test.json`

```JSON
{
    "extends": "./tsconfig.json",
    "compilerOptions": {
        "allowJs": true
    }
}
```

## DONE - Run the Test

Now we should be good to go:

```sh
$ npm run test

...

 PASS  src/__tests__/index.test.js
  index
    ✓ Responds correctly (6 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        3.234 s
Ran all test suites.
```

# Troubleshooting

In jest.config.js:

- having a `projects` setting was causing failures. (Fix: Remove it.)
- you can set `preset` to `ts-test` which is supposed to add `allowJs` to the tsconfig, but it doesn't seem to work. (Fix: use a tsconfig.test.json like we did above.)
- make sure the regex for the ts-jest `transform` includes file names with both `.ts` and `.js` extensions.

# References

- [Configuring Jest](https://jestjs.io/docs/en/configuration.html)
- [TypeScript Deep Dive Jest](https://basarat.gitbook.io/typescript/intro-1/jest)
- [facebook/jest issue](https://github.com/facebook/jest/issues/4842#issuecomment-469039359)
- [stackoverflow "ts-jest does not recognize es6 imports"](https://stackoverflow.com/questions/52173815/ts-jest-does-not-recognize-es6-imports)
