# Converting JS to TS for LWC app

## Prerequisites

1. `yarn global add typescript`
1. Add the following to `package.json`

```json
{
  "devDependencies": {
    "ts-jest": "^27.0.3",
    "typescript": "^4.5.4"
  }
}
```

## Converting `server` folder

1. Add `tsconfig.json`

```json
{
  "compilerOptions": {
    "noUnusedLocals": true,
    "declaration": true,
    "module": "commonjs",
    "moduleResolution": "node",
    "esModuleInterop": true,
    "target": "es2018",
    "outDir": "../../lib/server"
  },
  "exclude": ["**/__tests__"]
}
```

2. Rename `.mjs` files to `.ts`
3. Update any `.mjs` imports by removing the extension
4. Test with `tsc -b ./src/server`, fix any issues.
5. Add TypeScript checks to `tsconfig.json`, keeping other settings intact:

```json
{
  "compilerOptions": {
    "strict": true,
    "strictNullChecks": false, // This is needed for uninitialized variables
    "noImplicitAny": true,
    "noImplicitReturns": true,
    "noImplicitThis": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true
  }
}
```

1. Fix missing type errors. If no `@types` package exists, add a folder `typings` under `server` and a new declaration (.d.ts) file containing `declare module 'MODULENAME';` and replace MODULENAME with the name of the missing module.
2. `TS6133: 'VARIABLE' is declared but its value is never read.`. Remove unused variables or prefix them with underscore (`_`).
3. `yarn add @types/express --dev` and add types to `req` and `res` variables: `express.Request` and `express.Response` respectively, where `express` is the default import.
4. `yarn add @types/cors --dev`

`tsc --init --strict`

5. Rename `.js` files to `.ts`
6. For LWC components, add `@track` to class fields used in views. (In TypeScript, apparently-unused variables are removed, and the annotation protects them)
7. Use `as` to cast types where needed
8. Prefix private member variables with `_` and add `private` modifier. Use `readonly` as applicable.
9. Specify return types to functions and methods. Use `void` if no return.
