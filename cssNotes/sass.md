createdAt: "2020-02-06T16:20:32.532Z"
updatedAt: "2020-02-07T20:21:51.499Z"
type: "MARKDOWN_NOTE"
folder: "7b7225fb954665754643"
title: "Sass and how to use it"
tags: [
  "css"
  "npm"
  "sass"
]
content: '''
  # `Sass` and how to use it
  - `Bootstrap 4+` is use `Sass`
  
  ## Install the `npm` `node-sass` module
  - run `npm install --save-dev node-sass` in the terminal
  - open your `package.json` file for editing
  - in the `scripts:` section add the line
  - `"scss": "node-sass -o css/ css/"` (don't forget to add `,` to the end of the line above if there is none)
  - this specifies that both the source and the destination folder will be the css folder, all the `.scss` files there will be converted to `.css` files when you run the script
  
  ## Create your `Sass` file:
  - in your css folder create a `styles.scss` file
  
  ## Convert you `Sass` file to regular `css` file
  - in your teminal `cd` into your project folder
  - run `npm run scss`
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
