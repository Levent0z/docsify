# JEST

## Structure

file.test.js

```javascript
describe('description' () => {
    const sharedVar = 'shared value';

    it('test case', () => {
        /* expect */
    });
});
```

## Basic Tests

```javascript
it('Example', () => {
    expect(result).toBeDefined();
    expect(result).toBeUndefined();

    expect(result).toBeTruthy();
    expect(result).toBeFalsy();
    expect(result).toBe(expectedValue);
    expect(result).toEqual(expectedValue);
    expect(result).toBeLessThanOrEqual(expectedValue);
    expect(result).toMatchObject(similarObject);

    expect(someArray).toHaveLength(expectedLength);
});
```

## Type Checks

```javascript
expect(result).toEqual(expect.any(String));
expect(result).toEqual(expect.any(Number));
expect(result).toEqual(expect.any(Object));
expect(result).toMatchObject({
    someField: expect.objectContaining({
        someMap: expect.any(Map),
        someField: undefined,
    }),
    response: expect.any(Response),
});
```

## Create a mock function

```javascript
const func = jest.fn();
const funcWithImplementation = jest.fn(() => {});
expect(func).toHaveBeenCalled();
```

## Spying a method

```javascript
const spy = jest.spyOn(someObject, 'methodName');
spy.mockImplementationOnce(
    jest.fn(() => {
        return false;
    })
); // Override implementation to prevent "UnhandledPromiseRejection"

expect(spy).toHaveBeenCalled();
expect(spy).not.toHaveBeenCalled();
expect(spy).toHaveBeenCalledTimes(1);

spy.mockClear();
spy.mockReset();
spy.mockRestore();
```

## Function tests

```javascript
expect(spy).toHaveBeenCalledWith(
    expect.any(String),
    expect.any(Number),
    expect.any(Object),
    expect.any(Error)
);
// Also can use .toHaveBeenLastCalledWith()

expect(spy).toHaveBeenCalledWith(
    localhost,
    expect.objectContaining({
        method: 'POST',
        body: expect.any(FormData),
    })
);
```

## Mocking a module

```javascript
const originalModule = jest.requireActual('path/to/module');
jest.mock('path/to/module', () => {
    return Object.assign({}, originalModule, {
        export1: {
            newMethod: () => {},
            existingMethod: () => {},
        },
    });
});

import { export1 } from 'path/to/module';
```

In Jest, hoisting of imports is not strict.

## Dealing with time

```javascript
describe('time tests', () => {
    const timeout = () => jest.advanceTimersToNextTimer();
    const timeoutIn = (msecs) => jest.advanceTimersByTime(msecs);

    beforeEach(() => {
        jest.useFakeTimers();
    });

    afterEach(() => {
        jest.useRealTimers();
    });
});
```

## Dealing with fetch

```javascript
import { enableFetchMocks, disableFetchMocks } from 'jest-fetch-mock';

describe('fetch tests', () =>
    beforeAll(() => {
        enableFetchMocks();
    });
	{
	beforeEach(() => {
        fetchMock.resetMocks();
    });

    afterAll(() => {
        disableFetchMocks();
    });

	it(() => async {
		fetchMock.mockResponseOnce(async () => {
            throw error;
        });
		expect(spy).toHaveBeenCalledWith(
			localhost,
			expect.objectContaining({
				method: 'POST',
				body: expect.any(FormData),
			})
		);
	});
});
```

## Spying on Global Variables

```javascript
const nowSpy = jest.spyOn(Date, 'now');

const performanceSpy = jest.spyOn(globalThis, 'performance', 'get');
const navigatorSpy = jest.spyOn(globalThis, 'navigator', 'get');
```

## Testing Exceptions

```javascript
it('exceptions', () => {
    expect(() => methodToTest()).toThrow();
    expect(() => methodToTest()).not.toThrow();
});
```

## Async tests

```javascript
describe('async tests', () => {
    it('async test', async () => {
        await expect(someAsyncMethod()).resolves.toBe(expectedValue);
        await expect(someAsyncMethod()).resolves.toMatchObject(similarObject);
        await expect(someAsyncMethod()).rejects.toThrow();
    });
});
```

jest.mock
jest.isolateModules
mock modules?

```javascript
jest.mock('package/module', () => ({}), { virtual: true });
```

`__esModule` is needed for module with default exports


expectDefine()

https://www.npmjs.com/package/memfs
directory structure (**tests**)

Reaching into past function calls
const retValue = spyFunc.mock.results[0].value;
mockReturnValue
spyFunc.mock.calls[0][0] // first argument to first call

slide from Matrix 2

jest.config.js:

```javascript
module.exports = {
    // resolver,
    displayName: 'display name',
    preset: 'some-jest-preset',
    moduleNameMapper: {
        '^module/(.+)$': '<rootDir>/../node_modules/module/$1',
    },
    transformIgnorePatterns: ['node_modules/someRegexPattern'],
    testURL: 'https://localhost',
    testMatch: ['<rootDir>/**/__tests__/*.(spec|test).(ts|js)'],
};
```


If you make changes to jest.config.js, restart Jest runners in vs code.
