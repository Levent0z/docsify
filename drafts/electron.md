o>./node_modules/electron/dist/Electron.app/Contents/MacOS/Electron

```
Electron 10.1.1 - Build cross platform desktop apps with JavaScript, HTML, and CSS
Usage: electron [options] [path]

A path to an Electron app may be specified. It must be one of the following:
  - index.js file.
  - Folder containing a package.json file.
  - Folder containing an index.js file.
  - .html/.htm file.
  - http://, https://, or file:// URL.

Options:
  -i, --interactive     Open a REPL to the main process.
  -r, --require         Module to preload (option can be repeated).
  -v, --version         Print the version.
  -a, --abi             Print the Node ABI version.
  ```


# Use Create-LWC-App to create an Electron LWC-app

```bash
npx create-lwc-app clowder
```
Don't use simple setup. When asked "Select the type of app you want to create", choose "Electron app".