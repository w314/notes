createdAt: "2021-04-10T15:51:30.275Z"
updatedAt: "2021-04-10T16:05:27.605Z"
type: "MARKDOWN_NOTE"
folder: "1325bee4689e3ec8bae8"
title: "CSS Calc"
tags: [
  "css"
  "calc"
]
content: '''
  # CSS Calc
  - can combaine measurements like `%` and `px`
  - **needs strict formatting to work**
    - must have spaces around operators
    - cannot have spaces between `calc` and `(`
  ```css
  div {
    width: calc(100% - 30px);
  }
  ```
  - useful with variables
  ```css
  div {
    --width: 100px;
    width: calc(var(--width) * 2);
  }
  ```
  - can be used to calculate complementary colors
  ```css
  :root {
    --hue: 180;
  }
  
  .primaryButton {
    background-color: hsl(var(--hue), 100%, 50%);
  }
  
  .dangersButton {
    background-color: hsl(calc(var(--hue) - 180), 100%, 50%)
  }
  ```
  
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
