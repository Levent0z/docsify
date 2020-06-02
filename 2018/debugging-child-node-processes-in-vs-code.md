# Debugging Child Node Processes In VS Code

<details><summary style="font-size:1.5em">Prologue</summary>
Setting up debugging should be straightforward. In the case of child-process debugging for Node, it isn't. Like the proverbial planets, all the configurations have to align. However, once setup, the full-power of the debugger with breakpoints, watches, call-stacks and immediate-windows will be at your disposal. Say goodbye to console logs!
</details>

## TL;DR
To enable child process debugging for Node, the child Node process must be launched with certain arguments. In addition, if using VS Code, the editor should be configured to auto-attach to child processes.


## Command-line arguments for Node
The arguments that worked for me are "--nolazy --inspect --inspect-port=9230 --inspect-brk". By default Node debugging starts at port 9229, so it's already in use for the parent process if you're launching your project in debug mode. We must tell the child-process to use a different port. If you have multiple child-processes running at the same time, they should all have their unique inspect ports, or debug attach will silently fail.

```JavaScript
const cp = require('child_process');
const childProc = cp.fork('path_to_js_file', {
    execArgv: ['--nolazy', '--inspect', '--inspect-port=9230', '--inspect-brk']
});
```

- `--inspect`: Indicates that we want to use the more recent debugging protocol
- `--inspect-port`: Defines the debugging port
- `--nolazy` and `--inspect-brk` are there for fast-running processes to be debugged. Otherwise, the child process may spawn, run and terminate before the debugger has had a chance to auto-attach.

## VS Code Configuration

To enable automatic debug attaching to Node processes, enable the following in your current debug configuration. 

```JSON
"autoAttachChildProceesses": true
```

Also, you should enable the auto-attach in Debug mode using the command palette (CTRL+E/CMD+SHIFT+P):

```
>Debug: Toggle Auto Attach
```

which will add  
```json
"debug.node.autoAttach": "on"
```
to your Workspace settings.


## Gotchas

### Orphaned processes
Sometimes during development, as you start and stop processes, you may find that there are orphaned node processes in Task Manager (Windows) or Activity Monitor (Mac). These processes will hold onto their configured inspect ports and any new spawning of processes using those ports will silently fail debug attachment. Node processes are typically names "Node" in the process list, but can also have different names based on your project configuration.

### Different methods of launching child process in Node
There are several methods of launching a child process in Node. The most flexible and the most powerful is the __spawn__ function, and it allows launching any process. If you want to launch a Node process, the __fork__ function is more convenient. These functions' signatures vary greatly and care must be taken to ensure the arguments are passed to Node correctly. This is especially true for spawn, as ordering of the arguments matters: 

```sh
node [arguments to node] script.js [arguments to the script]
```

<details>
<summary>More Reading</summary>
<ul>
<li><a href="https://nodejs.org/en/docs/guides/debugging-getting-started/">Node Debugging Guide</a></li>
<li><a href="https://code.visualstudio.com/docs/nodejs/nodejs-debugging">Node.js debugging in VS Code</a></li>
<li><a href="https://code.visualstudio.com/blogs/2018/07/12/introducing-logpoints-and-auto-attach">Introducing Logpoints and auto-attach</a></li>
</details>