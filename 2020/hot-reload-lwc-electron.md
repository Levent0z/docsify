# How to Hot Reload your LWC-based Electron App

If you've created your Lightning Web Components app using  `create-lwc-app`, your package.json already has the ability to hot reload (aka live reload) any changes you make to the source. This functionality, initiated by `npm run watch` only works when you're using the provided localhost web server. It doesn't work for Electron.

What we want is to have `lwc-services` build the project so that the artifacts are deployed to the local `dist` folder where Electron is sourcing them from. Here are the steps:

1. Watch for changes in the `src` folder
2. Upon changes, call `npm run build:development` which will in turn `lwc-services build` and deploy binaries to `dist`.
3. We need Electron itself to be watching changes to the `dist` folder so it can reload itself.

So let's get to it. 

1. First acquire the NPM package [electron-reload](https://www.npmjs.com/package/electron-reload). From the root of your project, do:

```bash
> npm install electron-reload
```

2. In `scripts/main.js`, add the following near the top of the file:

```JavaScript
const distPath = path.join(__dirname, '..', 'dist');

require("electron-reload")(distPath, {
    electron: path.join(__dirname, '..', 'node_modules', '.bin', 'electron'),
});
```

3. In `lwc-services.config.js`, set [noclear](https://github.com/muenzpraeger/create-lwc-app/blob/main/packages/lwc-services/example/lwc-services.config.js#L11) to true. With this, lwc-services will overwrite files as opposed to deleting them first. 

```JavaScript
module.exports = {
    resources: [{ from: 'src/resources/', to: 'dist/resources/' }],
    noclear: true
};
```

4. Install [fswatch](https://github.com/emcrisostomo/fswatch), which is a cross-platform command-line tool that monitors a folder and outputs the changes the `stdout`.

```bash
> brew install fswatch
```

5. In a separate terminal window, in the root project folder, run the following:
```bash
> fswatch src | while read; do npm run build:development; done
```

6. Run Electron
```bash
npm run start 
```

7. In your code editor, make a change to the file. After a few seconds, the app should reflect the changes. 

## Troubleshooting: 
If something doesn't work right, here's a few things to look at:

- Ensure that the paths are correct in `main.js`
- Check the scripts in `package.json`
- Make sure that when you make a change, lwc-services rebuilds the code, and that code ends up in the `dist` folder.
- See if any [chokidar](https://github.com/paulmillr/chokidar) options will help. (Electron-reloader accepts the same properties in the object passed as the 2nd argument in the `require` line). For example, `awaitWriteFinish` option allows to override defaults.

And for reference here's my environment:

|| version | 
| --- | --- |
| macOS | 10.15.6 |
| npm | 6.14.8 |
| node | 14.10.0 |
| electron | 10.1.1 |
| electron-reload | 1.5.0 |
| lwc-services | 2.1.6 |
| fswatch | 1.15.0 |
