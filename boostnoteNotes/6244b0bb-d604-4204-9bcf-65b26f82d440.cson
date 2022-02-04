createdAt: "2020-01-28T21:39:33.567Z"
updatedAt: "2020-02-07T20:09:52.499Z"
type: "MARKDOWN_NOTE"
folder: "e6d3330423734e2f4fd6"
title: "lambda function in AWS"
tags: [
  "aws"
  "lambda"
]
content: '''
  ## `lambda` function in AWS
  
  `Lambda` is a serverless technology.
  
  ### Create a `Lambda` function
  - Search for `lambda` on the `Management Console` page
  - Click `Create Function` on AWS Lambda Dashboard
  - Select `Author from scratch`
  - Add `Function name`
  - Select `Node.js` as `Runtime`
  - For `Permissions` click `Choose or create an execution role`
  - Select `Create a new role with basic Lambda permissions`
  - Click `Create Function`
  
  ## Modify a `Lambda` function
  - After the function is created aws will display it on the screen. Scroll down to the code section.
  - Replace the code on line 5 with the code:
  ```js
  body: JSON.stringify('Hello ' + event.key1 + ' from Lambda!'),
  ```
  - Click `Save` in the upper right corner
  - Scroll down to `Basic Settings` and click `Edit`
  - Enter 'Udacity Function' as `Description`
  - Change `Timeout` from 3 seconds to 10 minutes
  - Click `Save`
  
  
  ## Test a `Lambda` function
  
  - Click on the `Test` button in the upper right corner
  - Ensure that the `Event template` is: Hello World
  - Enter 'TestEvent' (no spaces) as the `Event name`
  - Update the code to the one below:
  ```json
  {
  "key1": "Place your name here"
  }
  ``` 
  - Click `Create`
  - Click `Test` in upper right corner
  - You'll see your `Execution results` on top of the page
'''
linesHighlighted: []
isStarred: false
isTrashed: false
