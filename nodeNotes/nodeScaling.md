# Scaling in NodeJs

- node is single threaded
- to use multiple processor node has built in modules 
- handled with built-in modules
    - `child_process`
    - `cluster`

## `child_process module`

Used to create child processes to leverage a multi-core CPU based system.

### main methods of the child_process module
- exec
- spawn
- fork

### `exec()` method
- `exec(command, [options], callback)`
- launches a child process
- runs the given comman in a shell
- uses buffer

### `spawn()` method
- `spawn(command, [args], [options])`
- uses the operation system process creation method
- launches new child process
- returns a child process object
- uses buffer

### `fork()` method
- `fork(modulePath, [args], [options])`
- special from of `spawn()`




## execFile
creates a child process that executes and application without using a buffer

## cluster module

- built on top of the `child_process.fork()` method
Does load balancing between child processes
- fork spawns new child process
- al promesses use the same port
- 

events
- `listening` event is fired when worker process is available