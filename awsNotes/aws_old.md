createdAt: "2020-01-29T18:30:45.467Z"
updatedAt: "2020-02-25T17:14:17.639Z"
type: "MARKDOWN_NOTE"
folder: "e6d3330423734e2f4fd6"
title: "Amazon Web Services what is what"
tags: [
  "aws"
]
content: '''
  ## Amazon Web Services what is what
  
  `AWS` Amazon Web Services
  
  `IP Address` Internet Protocol Address
  
  `ARN` Amazon Resourse Name
  
  #### AWS Global Infrastructure
  
  `Region` 
  - Part of AWS Global Infrastructure. Refers to a geographic location or an area on a map
  - Has several, at least two `Availability Zones` (`AZ`)
  - You deploy you application in the `Region` depending where your users are, to minimize latency
  
  `AZ` Availability Zone
  - a physical data center within a specific `Region`
  - a disctinct, isolated location within a geographic region, engineered to be isolated from failers
  
  `Edge Location`
  - mini data center
  - used solely to cache files closer to a user's location
  
  #### AWS Security
  
  `PII` Personally Identifiable Information
  
  `DDoS` Distributed Denial of Service
  - an attempt to make an application unavailable by overwhelming it with traffic from multiple sources
  
  `XSS` Cross Site Scripting
  - is a client side code injection attack
  - can change website content, or redirect to other website
  - has access to user's cookies, therefore can impersonate the user and gain access to sensitive information
  - can get access to user's geolocation, camera, files...
  
  `AWS Shield`
  - is a managed `DDoS` protection service
  - it runs always automatically
  - part of free standard tier
  
  `Firewall`
  - firewall is a network security mechanism that monitors and controlls incoming and outgoing network traffic based on preset security rules
  
  `AWS WAF` AWS Web Application Firewall
  - it guards who an access your application
  - can stop common web attack like:
    - SQL injection
    - cross site scripting
  - by reviewing the data being sent to your application
  - `AWS WAF` can protect websites not hosted in AWS through `CloudFront`
  - you can configure `CloudFront` to preset a custom error page when requests are blocked
  
  `MFA` Multi Factor Authentication
  
  `IAM` Identity & Access Management
  - is an AWS service that allows us to configure who can access our AWS account, services or even applications running in our account
  - is a global service and automatically available accross all regions
  
  
  
  `S3` Simple Storage Service
  - object storage
  - maximum object size 5TB
  - `MFA Delete` can be enabled on `S3` buckets
  
  `S3 Glacier`
  - storage class for archiving purposes
  
  `DynamoDB`
  - `NoSQL` database service
  - fully managed
  - serverless
  - supports key-value and document data models
  - synchronously replicates data acress `AZ`-s in an AWS `Region`
  - supports `GET/PUT` operations using a primary key
  
  `RDS` Relational Database Service
  - Relational Database Service, is an AWS service that aids the administration and management of databases
  
  `Redshift`
  - Cloud data warehousing service of AWS
  - Stores data in columnar format to aid fast querying
  - Delivers great performance by using machine learning
  - Helps manage big data
  - Encrypts your data in trasit and at rest 
  
  `CDN` Content Delivery Network
  - Content Delivery Network, speeds up the delivery of content by caching content in a data center close to the end user
  
  `CloudFront`
  - Amazon's global content delivery network (CDN)
  - Caches content in `Edge Locations`
  - End-users request are served from the closest `Edge Location`
  - Works with non AWS origin sources
  - Cache control headers determine how frequently `CloudFront` needs to check the origin for an updated version of your file
  - Maximum size of file that can be delivered is 20GB
  
  #### AWS Domain Name Service
  
  `DNS` Domain Name System
  
  `Route 53`
  - Is a DNS (Domain Name System) service
  - Allows you to register and manage a domain name
  - Routes internet traffic to the resources for your domain
  - Allows you to route users based on the user's geographic location
  - Checks the health of your servers
  - Scales automatically to handle spikes in DNS queries
  
  #### AWS Servers
  
  `EC2` Elastic Computer Cloud
  - Virtual server in the cloud
  
  `EC2 Auto Scaling`
  - Is a service that monitors your EC2 instances and automatically adjusts by adding or removing EC2 instances based on conditions you define
  - Sends information when launcing or terminating instances via `SNS` (Simple Notification Service)
  
  `EC2 Auto Scaling Group`
  - Contains a collection of `EC2` instances that share similar characteristics and are treated as a logical grouping
  
  `Elastic Load Balancer`
  - A service that balances load between two or more servers
  - Stands in front of a web server and provides:
      - reduncancy: if you lose a server, the load balancer will send requests to other working servers. This feature maintains continuous operation in an emergency.
      - good preformance: if a server starts having issues or bottlenecks the load balancer will add more servers to the pool of available servers. Auto scaling automatically adjusts capacity to maintain a steady state.
  - `Elastic Load Balancing` works with `EC2` instances, conatiners, IP addreses, and Lambda functions
  - You can configure `EC2` instances to only accept traffic from a load balancer
  
  `AWS Auto Scaling`
  - Different than `EC2 Auto Scaling`
  - Service to setup auto scaling of other services (like DynamoDB)
  
  #### AWS Notification
  `Notification`
  - message from system to user
  
  `Message`
  - are sent form one system to another
  
  `Publish/Subscribe Model`
  - in order for the users to be notified they have to sign up or subsrcibe first
  
  `SNS` Simple Notification Service
  - a cloud service that allows you to send notifications to your users
  
  `SQS` Simple Queuing Service
  - a fully managed message queuing service
  
  #### AWS Management
  
  `Cloud Trail`
  - A logging service that records all AWS API calls accouring in your account
  
  `Cloud Watch`
  - a service that monitors AWS resources and applications by collecting data in the forms of logs, metrics and events
  
  `Infrastructure as Code`
  - a way to describe and provision all the infrastructure resources in the cloud environment
  - you can stand up servers, databases, runtime parameters, resources based on scripts you write
  
  `Cloud Formation `
  - AWS `Infrastructure as Code` service
  
  `CLI` Command Line Interface
  - `CLI` allows you to access and control running in your AWS account from the command line
  
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
