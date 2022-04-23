# Lerna and Workspaces

Example `package.json`:

```json
{
    "name": "project-parent",
    "private": true,
    "devDependencies": {
        "jest": "^27.0.4",
        "lerna": "^4.0.0",
        "ts-jest": "^27.0.3"
    },
    "scripts": {
        "build": "lerna run build",
        "build:clean": "yarn clean && yarn build",
        "clean": "lerna run clean",
        "test": "jest --config ./jest.config.js",
        "test:clean": "yarn clean && yarn test"
    },
    "workspaces": {
        "packages": [
            "packages/*"
        ]
    }
}
```

Example `lerna.json`:

```json
{
  "packages": ["packages/*"],
  "version": "238.5.1",
  "npmClient": "yarn",
  "useWorkspaces": true,
  "command": {
    "publish": {
      "registry": "https://registry.npmjs.org/"
    },
    "version": {
      "allowBranch": ["master", "release/*([0-9])"],
      "changelog": false,
      "commitHooks": false,
      "exact": true,
      "forceGitTag": true,
      "forcePublish": "*",
      "signGitCommit": false,
      "signGitTag": false,
      "yes": true,
      "verifyAccess": false
    }
  }
}
```

Example root `jest.config.js`:

```javascript
module.exports = {
    collectCoverage: true,
    // clover will create clover.xml
    // json-summary creates coverage-summary.json
    // text-summary outputs a report to the console at the end of testing.
    coverageReporters: ['clover', 'json-summary', 'html', 'text-summary'],
    reporters: ['default'],
    coverageThreshold: {
        // https://jestjs.io/docs/en/configuration#coveragethreshold-object
        global: {
            branches: 95,
            functions: 99,
            lines: 99,
            statements: 99
        }
    },
    projects: [
        {
            displayName: 'PACKAGENAME',
            testEnvironment: 'jsdom',
            testMatch: ['<rootDir>/packages/PACKAGE/**/*.(spec|test).(ts|js)'],
            // https://jestjs.io/docs/en/configuration#transformignorepatterns-arraystring
            transformIgnorePatterns: ['\\.pnp\\.[^\\/]+$'],
            transform: {
                '^.+\\.(t|j)s$': 'ts-jest'
            },
            globals: {
                'ts-jest': {
                    tsconfig: '<rootDir>/packages/PACKAGE/tsconfig.test.json'
                }
            },
            moduleNameMapper: {
                'PACKAGE/SUBMODULE': '<rootDir>/packages/PACKAGE/SUBMODULE/index'
            }
        }
    ],
    maxWorkers: 2
};
```

> Lerna commands are affected by any respective options in lerna.json. For example, a CLI options of the form `--no-this-that` must correspond to the JSON form `thisThat: false`.

With the default settings (unless overridden), [lerna version](https://github.com/lerna/lerna/tree/main/commands/version) will:

1. change the version depending on versioning mode
   Note: If using "independent" mode, each package.json will be individually updated,
   and no message placeholders (`%s`) will be replaced. Versions will be part of the commit description.
2. commit the change with the specified message
3. push the change and tags

Example prerelease with Lerna:

```sh
yarn lerna version prerelease -m 'chore(release): publish %s'
```
