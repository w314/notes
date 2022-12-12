createdAt: "2020-02-03T14:18:21.566Z"
updatedAt: "2020-02-07T20:09:32.743Z"
type: "MARKDOWN_NOTE"
folder: "e6d3330423734e2f4fd6"
title: "AWS Notification"
tags: [
  "aws"
  "sns"
  "notification"
]
content: '''
  ## AWS Notification
  
  `Notification`
  - message from system to user
  
  `Message`
  - are sent form one system to another
  
  `Publish\\Subscribe Model`
  - in order for the users to be notified they have to sign up or subsrcibe first
  
  
  `SNS` Simple Notification Service
  - a cloud service that allows you to send notifications to your users
  - allows you to decople to notification logic from being embedded in your application
  - allows notification to be publish to a large number of subscribers
  - uses the publish\\subscribe model
  - subscriber can be a person or an other AWS service
  - notification to end user can be sent via
      - mobile push
      - text message
      - email
  - can publich messages to Amamzon SQS queues, AWS lambda functions, and HTTP\\S  webhooks
  
  `Queue`
  - a data structure that holds requests called messages
  - messages are commonly processed in order, first in, first out (`FIFO`)
  -  supporst asynchronous processing
  
  `SQS` Simple Queue Service
  - fully managed message queuing service
  - two types of message queues:
      - standard
        - best effort processing
        - may be processed several times
      - FIFO
        - processed in exact order
        - porcessed exactly ones
       
       
  ### Setting up an `SNS` topic
  
  #### Create an `SNS` topic
  - navigate to `SNS`
  - click on `Topics` in the left side panel
  - click `Create Topic`
  - enter `Name`
  - under `Access Policy`
      - for `Define who can publish messages to this topic` select `Everyone`
      - for `Define who can subscribe to this topic` select `Everyone`
  - click `Create Topic`
  
  #### Subscribe to a topic
  - click on topic name to open topic
  - click `Create Subscription` in `Subscription` section
  - for `Protocol` select `Email`
  - for `Endpoint` enter email that should receive the notifications
  - click `Create Subscription`
  - if you click on `Subscriptions` on the left side panel, you'll see the subscriptions created with 'Pending confirmation' status
  - after confimation the satus changes to 'Confirmed'
  
  #### Publish a message to a topic
  - click on `Topics` on the left hand side
  - select created topic
  - click `Publish Message`
  - enter `Subject`
  - under `Message Body` section enter you message in `Message body to send to the endpoint`
  - scroll down and click `Publish Message`
  - check if you got the message via email
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
