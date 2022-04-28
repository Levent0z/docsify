# NPM Cheatsheet

```bash
$ npm init # creates package.json
```

```bash
$ echo "registry='https://registry.npmjs.org'" > .npmrc
$ npm config get registry
# Note: if the current directory doesn't have package.json, it will ignore the local .npmrc and may report settings from a higher-level config file, such as user-specific one from ~/.npmrc.
```

```bash
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

To set the auth token, you can do:

```bash
AUTHTOKEN=`echo -n $NEXUS_USERNAME:$NEXUS_PASSWORD | base64`
npm config set 'NPMREGISTRY:_authToken' '${AUTHTOKEN}'"
```

```bash
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

## Publish

```
npm version NEWVERSION -m 'COMMITMESSAGE'
npm publish ./dist --loglevel verbose
```

## Upgrade NPM

```
npm install npm@latest -g
```

## Upgrade Node

Method 1, using Node Version Manager
(Updates node in $HOME/.nvm/versions/node, adds to path)

```
nvm install node --reinstall-packages-from=node
```

Method 2
Using brew, Updates node in /usr/local/bin/node

```bash
brew upgrade node
```

## Using badges in markdown

Example

```markdown
[![oclif](https://img.shields.io/badge/cli-oclif-brightgreen.svg)](https://oclif.io)
[![Version](https://img.shields.io/npm/v/doppler-cli.svg)](https://npmjs.org/package/doppler-cli)
[![Downloads/week](https://img.shields.io/npm/dw/doppler-cli.svg)](https://npmjs.org/package/doppler-cli)
[![License](https://img.shields.io/npm/l/doppler-cli.svg)](https://github.com/loz/doppler-cli/blob/master/package.json)
```

## Get version from package.json

npm -s run env echo '$npm_package_version'

## Using config vars in package.json

Prefix config key with `$npm_package_config_`:

```json
    "config": {
        "KEYNAME": "value"
    },
    "scripts": {
        "script": "cliname -argname=$npm_package_config_KEYNAME"
    }

```

## Check whether the current package version is already published

```bash
    PACKVER=`npm -s run env echo '$npm_package_version'` # Get version
    PACKNAME=`npm -s run env echo '$npm_package_name'` # Get package name
    npm view $PACKNAME@$PACKVER dist.tarball # Display the path if exists, nothing otherwise
```

[Lerna Commands](https://github.com/lerna/lerna/tree/main/commands)

[Migrating to Lerna](https://riner.codes/moving-a-component-library-to-lerna-part-1/)

## Publish Scoped

```bash
mkdir tmp
cd tmp
npm init # use packaage name = @MYSCOPE/test1
cat << EOFKEY > index.js
console.log('hello');
EOFKEY
npm login --registry=https://registry.npmjs.org --scope=MYSCOPE
npm pack
npm publish --registry=https://registry.npmjs.org --scope=MYSCOPE --access=public
```

## Publish non-scoped

- use a unique name in package.json that doesn't exist in NPM. (Don't prefix with `@`)
- follow the steps above (scope arg is ignored)
- Login to npmjs.com with the user that published the package
- Go to Organizations > Teams > developers > Packages
- Put in the name of the package and click `+ Add Existing Package`
- The package should now be available under the org

## Misc

When `NPM_CONFIG_PRODUCTION` is true, npm automatically runs all scripts in a subshell where `NODE_ENV` is "production".

```bash
npm whoami --registry='https://registry.npmjs.org'
sh "npm config set proxy $PROXYURL"
sh "npm config set https-proxy $PROXYURL"
```
