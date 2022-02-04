createdAt: "2020-02-03T14:35:26.764Z"
updatedAt: "2020-02-07T20:09:17.039Z"
type: "MARKDOWN_NOTE"
folder: "e6d3330423734e2f4fd6"
title: "AWS Management"
tags: [
  "aws"
  "management"
  "cloudtrail"
]
content: '''
  ## AWS Management
  
  `Cloud Trail`
  - A logging service that records all AWS API calls accouring in your account
  - Shows results for the last 90 days
  - automatically enabled and free
  - for extra charge can create up to 5 trails in an AWS Region
  
  ### `Cloud Watch`
  - a service that monitors AWS resources and applications by collecting data in the form of logs, metrics and events
  - metrics are provided automatically for a number of AWS producst and service
  - you can create `Cloud Watch` logs from `Lambda` functions
  - you can set alarms and create triggers to run your AWS services (like `Lambda`)
  
  #### Create a `Cloud Watch` rule
  - navigate to `Cloud Watch`
  - select `Rules` under `Events` on the left panel
  - click `Create Rule`
  - for `Service Name` select `EC2`
  - for `Event Type` select `EC2 Instance State-change Notification`
  - select `Specific state(s)` radio button
  - select `running` from the drop-down box
  - click `Add target` in the `Target` section on the right sid e of the screen
  - in the drop-down box change `Lambda function` to `SNS topic`
  - for the `Topic` select the created topic. (if your topic doesn't appear the `Access Policy - optional` section doesn't have the proper settings to allow other services to access the topic)
  - scroll down and click `Configure details`
  - enter `Name`
  - make sure `State` is `Enabled`
  - click `Create rule`
  
  #### Test `Cloud Watch` rule
  - navigate to `EC2`
  - launch new `EC2` server
  - when the instance state changes to `running` you should get an email
  
  
  #### Cleanup `EC2` instance and `Cloud Watch` rule
  - select your `EC2`, then `Actions` -> `Instance State` ->  `Terminate`
  - to disable `Cloud Watch` rule navigate to dashboard
  - select `Rules` under `Events` on the left side
  - click the radio button next to your rule
  - select `Actions` -> `Delete`
  
  
  ### `Infrastructure as Code`
  - a way to describe and provision all the infrastructure resources in the cloud environment
  - you can stand up servers, databases, runtime parameters, resources based on scripts you write
  
  `Cloud Formation`
  - AWS `Infrastructure as Code` service
  - allows you to model your entire infrastructure in a text file template
  - templates are using JSON or YMAL
  - you can use a blueprint or write from scratch
  - there is even a visual designer with drag and drop components
  - these scripts can be checked into version control 
  - you can still individually manage AWS resources that are part of a `Cloud Formation` stack
  
  #### Create `Cloud Formation` stack
  - navigate to `Cloud Formation`
  - select `Designer` in left hand panel
  - expand `S3` in the `Resource Type` section
  - select `Bucket` and drag it to the designer window on the right side
  - replace the JSON found in the `Properties` tab with the one below:
  ```JSON
  {
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "Basic S3 Bucket CloudFormation template",
    "Resources": {
      "S3BucketCreatedByCloudFormation": {
        "Type": "AWS::S3::Bucket",
        "Properties": {
          "AccessControl": "PublicRead"
        }
      }
    },
    "Outputs": {
      "BucketName": {
        "Value": {
          "Ref": "S3BucketCreatedByCloudFormation"
        },
        "Description": "Name of the newly created Amazon S3 Bucket"
      }
    }
  }
  ```
  
  - hit the refresh button in the upper right corner, so that the Designer is not out of date
  - in the CloudFromation Designer toolbar expand the document icon and click `Save`
  - in the dialog box select 'Local File' and click `Save`
  - in the Designer toolbar click the check icon to validate the template
  - `Template is valid` message will appear in the middle of the toolbar
  
  #### Deploy `Cloud Formation` stack
  - in `Cloud Formation` Designer Toolbar click the cloud shape create stack icon, the `Create Stack` screen appears
  - accept the defaults and click `Next`
  - enter `Stack name`
  - leave `Parameters` empty
  - click `Next`
  - leave defaults click `Next`
  - review stack and click `Create stack`
  - the stack `Status` will be `CREATE_IN_PROGRESS`
  - click the refresh icon, when `Status` changes to `CREATE_COMPLETE` the stack is deployed
  
  
  #### View the created S3 bucket
  
  #### Delete `Cloud Formation` stack
  - navigate to `Cloud Formation`
  - select the stack
  - click `Delete` (all resources will be deleted too)
  
  ## `CLI` (Command Line Interface)
  - `CLI` allows you to access and control services running in your AWS account from the command line
  - to use it, download, install and configure it
  - 
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
