```sh
$ npm init # creates package.json
```

```sh
$ echo "registry='https://registry.npmjs.org'" > .npmrc
$ npm config get registry
# Note: if the current directory doesn't have package.json, it will ignore the local .npmrc and may report settings from a higher-level config file, such as user-specific one from ~/.npmrc.
```

```sh
# first this
$ npm config rm proxy
$ npm config rm https-proxy
# then this
$ npm config set registry http://registry.npmjs.org/
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

```sh
npm version (major|minor|patch)  # Set the new version to a number
```


https://nodejs.dev/learn/find-the-installed-version-of-an-npm-package
npm list PACKAGENAME
npm list -g PACKAGENAME
npm list -g --depth 0


npm outdated
https://docs.npmjs.com/updating-packages-downloaded-from-the-registry

[npm update](https://docs.npmjs.com/cli/v6/commands/npm-update)
Updates outdated packages but
- ^ will not touch packages with major version < 1
- ^ will not upgrade to major versions

Manually update package.json then:
```
npm update packagename
```



caret semantics for version < 1.0.0

https://stackoverflow.com/questions/16073603/how-do-i-update-each-dependency-in-package-json-to-the-latest-version



npm completion >> ~/.bash_profile





```
yarn config set "strict-ssl" false
cat ~/.yarnrc

npm config set strict-ssl false
```

# Publish
```
npm version NEWVERSION -m 'COMMITMESSAGE'
npm publish ./dist --loglevel verbose
```

# Upgrade NPM
```
npm install npm@latest -g
```

# Upgrade Node
Method 1, using Node Version Manager
(Updates node in $HOME/.nvm/versions/node, adds to path)
``` 
nvm install node --reinstall-packages-from=node
```

Method 2
Using brew, Updates node in /usr/local/bin/node
```sh
brew upgrade node
```


