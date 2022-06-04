# Yarn

## Find linked packages

Search for symbolic links:

```bash
( ls -l node_modules ; ls -l node_modules/@* ) | grep ^l
```

## VSCode settings

```json
    "jest.jestCommandLine": "yarn jest --config ./jest.config.js",
```

## NPM --> Yarn
[Cheatsheet](https://classic.yarnpkg.com/en/docs/migrating-from-npm/)