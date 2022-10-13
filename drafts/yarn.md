# Yarn

## Find linked packages

Search for symbolic links:

```bash
( ls -l node_modules ; ls -l node_modules/@* ) | grep ^l
```

or 

```bash
ls -l ~/.config/yarn/link
```

## List globally install packages

```bash
yarn global list
```

## VSCode settings

```json
    "jest.jestCommandLine": "yarn jest --config ./jest.config.js",
```


## NPM --> Yarn
[Cheatsheet](https://classic.yarnpkg.com/en/docs/migrating-from-npm/)