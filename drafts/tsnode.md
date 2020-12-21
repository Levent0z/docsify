nodemon and ts-node

`package.json`
```json
    "nodemonConfig": {
        "watch": [
            "src/server/**/*.ts",
            "src/server/**/*.js"
        ],
        "ext": "ts",
        "ignore": [
            "src/**/*.spec.ts",
            "src/**/*.test.ts"
        ],
        "exec": "ts-node ./src/server/api.ts"
    }
```
