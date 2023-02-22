# Jest Test Lifecycle

## lifecycle.test.js

```javascript
describe('top level', () => {
    const topObj = {
        func: jest.fn(),
    };
    const topFuncSpy = jest.spyOn(topObj, 'func');

    beforeAll(() => {
        console.log('beforeAll: top level');
    });

    beforeEach(() => {
        jest.resetAllMocks();
        console.log('beforeEach: top level');
    });

    afterEach(() => {
        console.log('afterEach: top level');
    });

    afterAll(() => {
        console.log('afterAll: top level');
    });

    it('first test', () => {
        console.log('first test');
        expect(true).toBeTruthy();
        topObj.func();
        expect(topFuncSpy).toHaveBeenCalledTimes(1);
    });

    it('second test', () => {
        console.log('second test');
        expect(true).toBeTruthy();
        topObj.func();
        expect(topFuncSpy).toHaveBeenCalledTimes(1);
    });

    describe('nested level', () => {
        const nestedObj = {
            func: jest.fn(),
        };
        const nestedFuncSpy = jest.spyOn(nestedObj, 'func');

        beforeAll(() => {
            console.log('beforeAll: nested level');
        });

        beforeEach(() => {
            console.log('beforeEach: nested level');
        });

        afterEach(() => {
            console.log('afterEach: nested level');
        });

        afterAll(() => {
            console.log('afterAll: nested level');
        });

        it('first nested test', () => {
            console.log('first nested test');
            expect(true).toBeTruthy();
            topObj.func();
            expect(topFuncSpy).toHaveBeenCalledTimes(1);
            nestedObj.func();
            expect(nestedFuncSpy).toHaveBeenCalledTimes(1);
        });

        it('second nested test', () => {
            console.log('second nested test');
            expect(true).toBeTruthy();
            topObj.func();
            expect(topFuncSpy).toHaveBeenCalledTimes(1);
            nestedObj.func();
            expect(nestedFuncSpy).toHaveBeenCalledTimes(1);
        });
    });
});
```

## Output (abbreviated):

```
    beforeAll: top level
    beforeEach: top level
    first test
    afterEach: top level
    beforeEach: top level
    second test
    afterEach: top level
    beforeAll: nested level
    beforeEach: top level
    beforeEach: nested level
    first nested test
    afterEach: nested level
    afterEach: top level
    beforeEach: top level
    beforeEach: nested level
    second nested test
    afterEach: nested level
    afterEach: top level
    afterAll: nested level
    afterAll: top level

 PASS   lifecycle.test.js
  top level
    ✓ first test (6 ms)
    ✓ second test (4 ms)
    nested level
      ✓ first nested test (7 ms)
      ✓ second nested test (7 ms)

Test Suites: 1 passed, 1 total
Tests:       4 passed, 4 total
Snapshots:   0 total
Time:        1.912 s
```
