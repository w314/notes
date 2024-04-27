nodejs, npm, spa

# Other Front End Topics

## NodeJS & `NPM`

We install react and it's dependencies with NPM and run it in a NodeJS environment.

### NodeJS

>Open source run-time enviroment used to execute javascript outside of a web browser.

Has a large library of JS modules

### NPM (Node Package Manager)

>`NodeJS's` built in package manager.

- online repository for publishing open-source Node.js projects
- 

- allows for downloading and installing frameworks/libraries
- has `CLI`,  commands start with `npm` or `npx`

NPM commands
- `npm install` - installs dependencies
- `npm start` - starts the application



## Library vs. Framework
### Libraries
- libraries are light weight and flexible
- but more work as you have to do all the work a framework would do for you
### Frameworks
- large, may be forced to use parts you do not need
- opinionated, offer limited flexibility


## SPA (Single Page Applications)

- loads a single HTML page and all the necessary assets
- instead of requesting different HTML pages it just swaps out the content of the one we have
- slower to load, but faster when it is loaded (cashes all received data locally)
- you can use `code splittin` to `lazy-load` resources if initial load is too slow, supported by bundler like `Webpack`
