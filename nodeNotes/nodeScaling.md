# Scaling in NodeJs

- node is single threaded
- to use multiple processor node has built in modules 
- handled with built-in modules
    - `child_process`
    - `cluster`

## `child_process module`

Used to create child processes to leverage a multi-core CPU based system.

### main methods of the child_process module
- spawn
- exec
- fork

### `spawn()` method
- `spawn(command, [args], [options])`
- uses the operation system process creation method
- launches new child process
- returns a child process object
- uses buffer

`parent.js`
```js
// import module
import { spawn } from "child_process";

// use the spawn method to execute the child.js program
// in a separate child process
const childProcess = spawn("node", ["child.js"]);

// use the write method to send data to the child process
childProcess.stdin.write("hi");

// listen to data coming from child process
childProcess.stdout.on("data", (data) => {
    console.log(`Data received from child process: ${data}`);
});

// listening to child process errors
childProcess.stderr.on("data", (data) => {
    console.log(`Child process error: ${data}`);
});

// set function to execute when child process is completed
childProcess.on("exit", (exitCode) => {
    console.log(`Child process finished with exit code: ${exitCode}`);
});
```

`child.js`
```js
process.stdin.on("data", (data) => {
    console.log(`Data received from parent: ${data}`);
});
```

### `exec()` method
- `exec(command, [options], callback)`
- launches a child process
- runs the given comman in a shell
- uses buffer


### `fork()` method
- `fork(modulePath, [args], [options])`
- special from of `spawn()`
- uses the `send()` method to communicate with child process
- listens to the `message` event to get message from child proces



### execFile
creates a child process that executes and application without using a buffer

## cluster module

- built on top of the `child_process.fork()` method
Does load balancing between child processes
- fork spawns new child process
- al processes use the same port


### cluster module fork method

`cluster.fork([env])` spawns a new child process

### cluster module events

- `fork`
    - emitted when a new worker is forked
- `online`
    - emitted when the worker is running
- `listening` 
    - emitted when calling listen() from a worker
- `exit`
    - emitted when a worker is killed

### Syntax
```js
import cluster from 'cluster'
import http from 'http'
```

