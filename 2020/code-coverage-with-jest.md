# How to Add Code Coverage with Jest

Code Coverage is a great tool in a quality developer's belt, as it encourages writing unit tests that exercise larger parts of the code base, and in the process helps you find and fix bugs sooner.

In this blog, I pick up where I left off with [Jest with TypeScript](./jest-with-typescript.md) to show how to add Code Coverage with Jest. See the end result in this [Git repo](https://github.com/Levent0z/jest-and-typescript). 

## STEP 1: Add jest-html-reporter

```bash
$ npm i jest-html-reporter --save-dev
```

This will add the following line into the `devDependencies` section of package.json:

```
    "jest-html-reporter": "^3.2.0",
```

## STEP 2: Update Jest configuration

Add the missing lines in your scripts/jest.config.js file:

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
    },
    coverageThreshold: {
        "global": {
            "branches": 85,
            "functions": 85,
            "lines": 85,
            "statements": 85
        }
    },
    collectCoverage: true,
    coverageReporters: ["json", "html"],
    reporters: [
        "default",
        [
            "./node_modules/jest-html-reporter",
            {
                "pageTitle": "Jest Test report",
                "outputPath": "./jest-report/index.html",
                "includeFailureMsg": true
            }
        ]
    ]
};
```

## STEP 3: Run the Test

```bash
$ npm run test
```

This will generate 2 reports:

1.  A **test report** (`jest-report/index.html`) that shows passing and failing tests.
2.  A **coverage report** for all files (`coverage/index.html`) that shows code coverage for each file, which you can drill into to see line-by-line coverage report.

If your code coverage falls below the thresholds specified in the Jest configuration file, the test run will fail with an error message similar to the following:

```
Jest: "global" coverage threshold for branches (85%) not met: 84%
```


To see additional information about what individual coverage thresholds mean, refer to the [documentation](https://jestjs.io/docs/en/configuration#coveragethreshold-object).
