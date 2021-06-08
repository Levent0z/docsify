# Jest 

## Test arguments

```JavaScript
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
