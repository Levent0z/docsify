# Jest and ESM

https://bl.ocks.org/rstacruz/511f43265de4939f6ca729a3df7b001c

https://jestjs.io/docs/en/ecmascript-modules

// https://jestjs.io/docs/en/configuration#transformignorepatterns-arraystring
transformIgnorePatterns: [
    "/node_modules/(?!MODULESUBFOLDERNAME)",
    "\\.pnp\\.[^\\\/]+$"
]
