angular

# Angular

Current version is 18, notes are about version 15.

## To Start Angular Project

Troubleshoot:
if `ng` is not in your path you run commands with `npx ng ...`, npx knows where ng is.

### Install angular with:

`npm install -g @angular/cli@15`

<i>Current version is 18, the course was in 15 which is outdated.</i>

### Create new project
`npx ng new <project-name>`
- say yes to Routing
- select styling (css for now)


### Start application
- cd into your project folder
- run `ng serve`
- go to `http://localhost:2400` in your browser

OR

- run `ng serve --open` to open the browser automatically
- to use different port `ng serve --port 8185 --open`



## Compilation In Angular

### `AOT` (Ahead Of Time)
    - default since Angular 9
    - uses angular compiler `ngc`
    - compiles before runtime


Advantages of `AOT` Compilation:
- faster rendering
- finding erros at build time
- reduces injection attacks
- reduces size of angular framewokr

<br>

EARLIER: `JIT` (Just In Time)
- default till Angular 8
- TypeScript code gets compiled at build
- using the `tsc` TypeScript compiler
- angular codes gets compiled at runtime
- angular issues come up at runtime only


## View Engine - `Ivy`

Default rendering engine since Angular 9.

Makes components:
- `treeshakable` - removes unused code from the component
- `local` - only compiles modified components


## Basic CLI Commands

- `npm install -g @angular/cli`	
    - Installs Angular CLI globally
- `ng new <project name>`	
    - Creates a new Angular application
- `ng serve --open` 	
    - builds the application 
    - runs it on lite-server
    - launches a browser
- `ng generate <name>` 	
    - creates class, component, directive, interface, module, pipe and service
- `ng build`	
    - builds the application

### Important Files & Folders

- `node_modules/`	
    - Node.js creates this folder
    - puts all modules listed in package.json inside it.
- `src/`	
    - all the application related files
- `angular.json`	
    - configuration file for Angular CLI
    - configures among other things what files to be included during project build.
- `package.json`	
    - node configuration file
    - contains all dependencies
- `tsconfig.json`	
    - Typescript configuration file