# How to Build your own CLI command using OCLIF

[The Open CLI Framework](https://oclif.io/)

## Installation

```sh
$ npx oclif single FOLDERNAME
$ cd FOLDERNAME
$ ./bin/run
```

This runs Yeoman which asks you a number of questions to initialize a Node project. You can use JavaScript or TypeScript. As a testing environment, you can choose chai and mocha. As CI/CD, there are multiple options such as CircleCI and TravisCI.

The starter app has a number of flags already defined:

```sh
$ ./bin/run -h
describe the command here

USAGE
  $ doppler-cli [FILE]

OPTIONS
  -f, --force
  -h, --help       show CLI help
  -n, --name=name  name to print
  -v, --version    show CLI version
```

The following are equivalent:

```sh
$ ./bin/run -n Levent
$ ./bin/run -n=Levent
$ ./bin/run -nLevent
$ ./bin/run --name Levent
$ ./bin/run --name=Levent
```

All this built-in logic lives in `src/index.ts`. The 4 flags are defined in the [flags](https://oclif.io/docs/flags) member:

```TypeScript
  static flags = {
    // add --version flag to show CLI version
    version: flags.version({char: 'v'}),
    help: flags.help({char: 'h'}),
    // flag with a value (-n, --name=VALUE)
    name: flags.string({char: 'n', description: 'name to print'}),
    // flag with no value (-f, --force)
    force: flags.boolean({char: 'f'})
  }
```

Any values passed after the flag char prefixed with a single dash (e.g. '-n') or the name of the key prefixed with double dashes (e.g. '--name') will be available as a member of the `flags` object. If you use special characters in a flag, `such-as-this-one`, simply use quotes around it when defining, and use the dictionary method when accessing.

The last argument is saved into `args.file`, due to this configuration of the [args](https://oclif.io/docs/args) member:

```TypeScript
  static args = [{name: 'file'}];
```

We access the runtime values of flags and args by desconstructing the return value of the `parse` method:

```TypeScript
    const { args, flags } = this.parse(DopplerCli);
```

When we run `./bin/run`, the shell knows that this file needs to be launched with Node (due to the shebang at the top). This also installs a global error handler implemented by oclif.

In order for debugging of `.ts` files, comment out the `"composite": true` line from the `tsconfig.json` file in the root folder of the project.

## Creating a Distributable Package

Before packaging make sure to run the following:

```sh
npm run prepack                  # Clean the lib folder and rebuild with TSC
npm version (major|minor|patch)  # Set the new version to a number
```

To create a package for macOS do:

```sh
oclif-dev pack:macos
```

Watchout:
When throwing exceptions, throw `Error` instances, not regular strings. Otherwise, when exceptions get caught by oclif's error handler (code is in `bin/run`) the error will appear to be silently swallowed. 