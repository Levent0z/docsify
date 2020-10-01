```sh
$ npm init # creates package.json
```

```sh
$ echo "registry='https://registry.npmjs.org'" > .npmrc
$ npm config get registry
# Note: if the current directory doesn't have package.json, it will ignore the local .npmrc and may report settings from a higher-level config file, such as user-specific one from ~/.npmrc.
```

## Example contents of .npmrc
```
//npm-url-path/:always-auth=true
//npm-url-path/:_authToken="gobbledygook"
//npm-url-path/:email=user@domain
cafile=/absolute/local/path/somefile.pem
registry=https://registry.npmjs.org
```

To get the authtoken, you can do:
```
echo -n USERNAME:PASSWORD | base64
```
