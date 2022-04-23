# Jest 

## Test arguments

```javascript
const spy = jest.spyOn(global, 'fetch');
// Work
expect(spy).toHaveBeenCalledWith(
    'http://127.0.0.1',
    expect.objectContaining({
        method: 'POST',
        body: expect.any(FormData)
    })
);
```


## Jest and ESM

https://bl.ocks.org/rstacruz/511f43265de4939f6ca729a3df7b001c

https://jestjs.io/docs/en/ecmascript-modules

// https://jestjs.io/docs/en/configuration#transformignorepatterns-arraystring
transformIgnorePatterns: [
    "/node_modules/(?!MODULESUBFOLDERNAME)",
    "\\.pnp\\.[^\\\/]+$"
]


## Before all

> Here the beforeAll ensures that the database is set up before tests run. If setup was synchronous, you could just do this without beforeAll. The key is that Jest will wait for a promise to resolve, so you can have asynchronous setup as well.


[API docs](https://jest-bot.github.io/jest/docs/api.html)

