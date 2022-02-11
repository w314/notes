createdAt: "2020-01-24T18:58:41.279Z"
updatedAt: "2020-12-01T16:00:00.439Z"
type: "MARKDOWN_NOTE"
folder: "7b7225fb954665754643"
title: "Bootstrap"
tags: [
  "bootstrap"
  "npm"
]
content: '''
  # Bootstrap
  - bootstrap is a `Front End Web UI Framework`
  - help to build mobile first responsive web sites
  - helps with cross-browser compatibility
  
  #### Set up your project to use npm
  [Node.js project, how to start one](:note:0bbbd620-7c3d-4f81-8d05-9467bfb9ce38)
  
  
  #### Use npm to install Bootstrap
  - in your project folder run: 
  `npm install bootstrap --save`
  - As bootstrap is dependent on JQuery and Popper.js also run:
  `npm install jquery popper.js --save`
  
  
  
  #### Set up your web page to use Bootstrap
  1. in the `<head>` section
    - Link Bootstrap as stylesheet:
  ```html
  <link rel="stylesheet" href="./node_modules/bootstrap/dist/css/bootstrap.min.css">
  ```
  
  2. in the `<script>` section
  Add js components as `<script>` just above the closing `</body>` tag in the following order: jquery first, then pooper, than bootstrap.
  ```html
  <script src="node_modules/jquery/dist/jquery.slim.min.js"></script>
  <script src="node_modules/popper.js/dist/umd/popper.min.js"></script>
  <script src="node_modules/bootstrap/dist/js/bootstrap.min.js"></script>
  ```
  
  ### Grid system
  - to use the `grid` system you have to enclose you content into a `.container` class
    
  
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
