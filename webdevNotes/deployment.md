createdAt: "2020-02-13T17:40:13.522Z"
updatedAt: "2020-02-29T16:28:49.439Z"
type: "MARKDOWN_NOTE"
folder: "0502aa55141f2315e808"
title: "Deployment"
tags: [
  "web_development"
  "deployment"
  "minification"
  "concatenation"
  "uglification"
  "task_runner"
  "grunt"
  "gulp"
]
content: '''
  # Deployment
  
  Web development consists of several repeptitive tasks that we want to automate.
  
  ## Task Runners
  The primary task of a task runner to enable us to configure the tasks and then rerun them automatically.
  `Grunt` and `Gulp` are task runners.
  
  ## Web development tasks
  
  ### CSS Tasks
  - compailing `Sass` or `Less` into `CSS`
  - running Autoprefixer to add any vendor prefixes that are needed
  - minifaction (removing unnecessary characters: white spaces, new line, comments)
  - concatenation (merging several css files into one)
  
  ### JavaScript Tasks
  - `JSHint`, checking JavaScript code for errors
  - concatenation to minimize the number of downloads needed
  - uglification: minification + mangling (reduce local variables to single letters)
  
  ### Other tasks
  - images: optimizing files to reduce file size
  - watch: watching for changes in files and automatically rerunnig tasks
  - server and livereload (to follow changes during development, `lite server` is a solution for that)
  - testing
  - building site for deployment also called builing up distribution files
  
  
  ## Automate tasks by `NPM Scritps`
  - found in the `scripts` property in the `package.json` file
  - `npm start` will run the script under `"start":`
  - other scripts can be run by the `npm run <scriptName>`command
  
  ### Setup file watch
  - A scripts is needed to watch file for any changes so when a change happens it can trigger the necessary scripts
  - The `Watch` npm module could be used for this purpose
  - We instlall the `Onchange` npm module to do the job
    - run `npm install install --save-dev onchange`
    - in `package.json` add to the `scripts` property the line:
    `"watch:scss": "onchange 'css/*.scss' -- npm run scss"`
    (in windows use `\\"css/*.scss\\"`)
    When `npm run watch:scss` is run later, it will watch every `.scss` file in the `css` directory and if any changes happen it will run `npm run scss` to update the css files.
  
  ### Setup running multiple scripts at once
  #### `Parallelshell`
  - `Parallelshel` allows us to execute multiple npm scritps in paralell shells
  (`concurrently` npm module can be used for the same purpose)
  - To install it run: `npm install --save-dev parallelshell`
  - In `package.json` add to the `scripts` property:
  `"watch:all": "parallelshell 'npm run watch:scss' 'npm run lite'"`
  (use `\\"` instead of `'` on windows)
  - **fix bug in parallelshel (3.0.2)** : 
    - in `node_modules/parallelshell/index.js:105`
    - change:
    `cwd: process.versions.node < '8.0.0' ? process.cwd : process.cwd(),`
    - to:
    `cwd: parseInt(process.versions.node) < 8 ? process.cwd : process.cwd(),`
    - as the corrected file is in `.gitignore`, our change is not saved whenever we would recreate the environment with `npm install` we would **have to fix the problem manually each time** again 
  - to use paralellshell change `"start"` in the `scripts` property to:
  `"start": "npm run watch:all"`
  
  #### `Concurrently`
  - if `Parallelshell` is already installed run `npm uninstall parallelshell --save-dev`
  - to install run `npm install concurrently --save-dev`
  - change `"watch:all"` line in scripts to:
  `"watch:all": "concurrently 'npm run watch:scss' 'npm run lite'"`
  (use `\\"` for `'` in windows) 
  
  ### Create files for deployment
  
  #### Setting up a `dist` (distribution) folder
  - it contains all the files for our project so that we can simply deploy to a web server that hosts our website.
  - add the `dist` folder to `.gitignore`
  
  #### Cleaning our dist folder
  - will need a script the will delete and rebuild our distribution folder each time we rebuild it after changing our project, we'll use `rimraf`:
  `npm install --save-dev rimraf`
  - `rimraf` will help to clean out a folder completely
  - add a new `script` in `package.json` file
  `"clean": "rimraf dist"`
  where "dist" is the name of your distribution folder
  
  #### Copying files
  - install `copyfiles` `npm` module for copying files from one folder to an other:
  `npm -g install copyfiles`
  - we'll need font-awesome files to be available when our page is rendered
  - in the `package.json` file under `scripts` add:
  `"copyfonts": "copyfiles -f node_modules/font-awesome/fonts/* dist/fonts"`
  `-f` means:"copyfiles -f node_modules/font-awesome/fonts/* dist/fonts" copy files without the hieararchy
  it will create a `dist` directory with a subdirectory `fonts` and copy the font-awesome files there
  
  #### Compressing and Minifying images
  - install `imagemin` `node` module:
  `npm -g install imagemin-cli`
  - in `package.json` file add the script:
  `"imagemin": "imagemin img/* -o dist/img"`
  where `img/*` is the folder with your images
  
  #### Preparing the distribution folder
  - install `node` module `usemin-cli`
  - does the modification of html files
  - concatenates and combines all css files to one and copies it to distribution folder
  - does the same with javascript files
  - to do the job `usemin` uses three other modules
    - `cssmin`
    - `uglifyjs`
    - `htmlmin`
  - to install run:
  `npm install --save-dev usemin-cli cssmin uglifyjs htmlmin`
  - mark css files to use for `usemin` in all your html files:
  ```html
  <!-- build:css css/main.css -->
  <link rel="stylesheet" href="node_modules/bootstrap/dist/css/bootstrap.min.css">
  <link rel="stylesheet" href="node_modules/font-awesome/css/font-awesome.min.css">
  <link rel="stylesheet" href="node_modules/bootstrap-social/bootstrap-social.css">
  <link rel="stylesheet" href="css/styles.css">
  <!-- endbuild -->
  ```
  - mark all js files for `usemin` to process in all html files:
  ``` html
  <!-- build:js js/main.js -->
  <script src="node_modules/jquery/dist/jquery.slim.min.js"></script>
  <script src="node_modules/popper.js/dist/umd/popper.min.js"></script>
  <script src="node_modules/bootstrap/dist/js/bootstrap.min.js"></script>
  <script src="js/scripts.js"></script>
  <!-- endbuild -->
  ```
  - setup script in `package.json` file:
  `"usemin": "usemin contactus.html -d dist --htmlmin -o dist/contactus.html && usemin aboutus.html -d dist --htmlmin -o dist/aboutus.html && usemin index.html -d dist --htmlmin -o dist/index.html"`
  `-d` for destination folder
  `--htmlmin` minimize the html files removing comments
  `-o`
  - add build script in `package.json` to create distribution folder
  `"build": "npm run clean && npm run copyfonts && npm run imagemin && npm run usemin"`
  
  ## `Grunt`
  `Grunt` is a task runner that concentrates on configuration over code.
  
  ## `Gulp`
  `Gulp` is a taks runner that concentrates on code over configuration.
  
  
  
'''
linesHighlighted: [
  83
]
isStarred: false
isTrashed: false
