createdAt: "2020-01-28T23:29:59.732Z"
updatedAt: "2020-02-07T20:09:42.218Z"
type: "MARKDOWN_NOTE"
folder: "e6d3330423734e2f4fd6"
title: "Elastic Beanstalk"
tags: [
  "aws"
  "elasticBeanstalk"
]
content: '''
  ## `Elastic Beanstalk`
  
  `Elastic Beanstalk` is an `AWS` is an orchestration service that allows you to deploy a web application by clicking a button that will provide all the services you need to run your application.
  
  ## Deploy application via `Elastic Beanstalk`
  - Find `Elastic Beanstalk` on `AWS Management Console`
  - Click `Get Started`
  - Enter `Application Name`
  - Choose `Tomcat` as `Platform`
  - Under `Application code` choose `Upload your code`
  - After choosing your file click `Upload` (uplead udacity.war)
  - Click `Create Application` (it will take about 10 minutes), when the
  - As soon as it created you'll see a dashboard showing that your application `Health` is `OK`.
  
  
  ## Test you application
  - From you application Dashboard copy the url of the application. It's on the top of the page right to the name of the application.
  - In a browser paste the url and append `/message` on the end
  - With this application you should see: Hello World
  
  ## Check `EC2` created
  - Navigate to the `EC2 Dashboard`
  - The `EC2` created will have the same name as the application
  
  ## Cleanup and delete resources
  - Navigate back the `Elastic Beanstalk`
  - Select your application
  - Select `Actions` -> `Terminate Environment`
  - Enter the name of the environment
  - Click `Terminate`
  - After the environment is terminated you will be shown the page of the application again
  - Select `Action` -> `Delete Application`
  - Enter the name of the application
  - Click `Delete`
  - (Looks like it doesn't delete the `S3 bucket` created)
'''
linesHighlighted: []
isStarred: false
isTrashed: false
