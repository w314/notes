aws, cloud, ec2

# AWS (Amazon Web Services)
> Service provided by Amazon which uses distributed IT infrastructure to provide different IT resources available on demand. 

AWS offers the building blocks of an IT infrastructure for individuals or companies to use… usually for a fee

## AWS Infrastrucure
### AWS Region
> Is a geographical location with a collection of availability zones mapped to physical data centres in that region.
- currently there are 27
- important for workloads that are **latency-sensitive**
- each region is physically isolated from and **independent** of every other region in terms of location, power, water supply, etc
- each has two or more availability zones

### AWS Availability Zone
>Is a logical data centre in a region.

Each zone in a region has redundant and separate power, networking and connectivity to reduce the likelihood of two zones failing simultaneously.

## RDS (Relational Database Service)
> Is a collection of managed services that makes it simple to set up, operate, and scale databases in the cloud.




## EC2 (Elastic Compute Cloud)
> EC2 (Elastic Compute Cloud) provides scalable computing capacity in the Amazon Web Services (AWS) Cloud.
- eliminates the need to invest in hardware upfront
- provides scalability

EC2 Types
### On-Demand Instances
- allows you to pay a fixed rate per hour with no commitment

### Spot Instances
- allows you to bid for a price 
- provides better savings if your application have felxible start and end times
### Reserved Instance
- useful when an application is at a steady state
#### Standard Reserved Instance
- provides discount up to 75%

#### Convertible Reserved Instance
- discount up to 54%
- you are allowed to upscale

#### Scheduled Reserved Instance
- available in the time window you reserved


### Dedicated Hosts
- a physical server just for one user.

### EC2 Autoscaling
Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application.

You create collections of EC2 instances, called Auto Scaling groups. 
- You can specify the minimum number of instances in each Auto Scaling group
- You can specify the maximum number of instances in each Auto Scaling group

Two types of auto-scaling are:
- Vertical Scaling(Scaling instances up & down)
- Horizontal Scaling(Scaling similar instances)



## S3 (Simple Storage Service)
> S3 is an object storage service.

- data is stored as individual objects rather than in some kind of hierarchy
- Each object is put into a bucket and you connect to Amazon S3 using a URL.
- The URL will have the name of your object and the name of your bucket. The bucket is just the container in which you put your objects.
- You use  a REST API to connect to S3 using a URL.
- Your browser does an HTTP PUT request and it puts the objects in the bucket.

### Use cases
- You can store any type of file in S3.
- Backup and Storage
- Application Hosting
- Media Hosting
- Software Delivery - host software apps that your customers can download
- Static Website Hosting - You can configure a static website to run from an S3 bucket.

### The different storage classes are:
- S3 Intelligent-Tiering - For automatic cost savings for data with unknown or changing access patterns
- S3 Standard - For frequently accessed data
- S3 Standard-Infrequent Access (S3 Standard-IA) - For   less frequently accessed data
- S3 One Zone-Infrequent Access (S3 One Zone-IA) - For   less frequently accessed data
- S3 Glacier Instant Retrieval - For archive data that needs immediate access
- S3 Glacier Flexible Retrieval (formerly S3 Glacier) - For rarely accessed long-term data that does not require immediate access
- S3 Glacier Deep Archive (S3 Glacier Deep Archive) - For long-term archive.


## Security Groups
> Security groups are used to control the inbound and outbound traffic on the EC2.
- A VPC comes with a default security group.
- You can associate a security group only with resources in the VPC for which it is created.
- you add rules that control the traffic based on protocols and port numbers

### VPC (Virtual Private Cloud)
> With Amazon Virtual Private Cloud (Amazon VPC), you can launch AWS resources in a logically isolated virtual network that you've defined. 

### ACL (Access Control List)
A network access control list (ACL) allows or denies specific inbound or outbound traffic at the `subnet` level.

-here are separate sets of rules for inbound traffic and outbound traffic.


## EBS (Elastic Block Store)
> EBS provides block level storage volume for EC2 instances.

- EBS provides durable block-level storage volumes for use with EC2 instances.
- EBS volumes are created in a specific Availability Zone
- EBS volumes can be backed to Amazon S3 by taking point-in-time snapshots.

#### What is block storage
>Block storage is technology that controls data storage and storage devices. 

It takes any data, like a file or database entry, and divides it into blocks of equal sizes. The block storage system then stores the data block on underlying physical storage in a manner that is optimized for fast access and retrieval.

## AMI (Amazon Machine Image)

>An Amazon Machine Image (AMI) is a supported and maintained image provided by AWS that provides the information required to launch an instance.

An AMI includes:
- One or more EBS snapshots.
- Launch permissions that control which AWS accounts can use the AMI to launch instances.
- A block device mapping specifies the volumes to attach to the instance when it's launched.


## SSH (Secure Shell)
SSH is a network protocol that gives users, particularly system administrators, a secure way to access a computer over an unsecured network.
- Your EC2 instance will be running in a public subnet. Your EC2 instance has a public address on the internet which you can access from wherever you have internet access.
- The relevant protocol by which we can access the instance is by using Secure Shell (SSH) which is the TCP protocol port 22.

## AWS Questions

Cloud Computing 

What is cloud computing? 

What are the different types of cloud computing models? 

What are the 3 different privacy models? 

What is AWS? Why is it like “Amazon filling a niche in our field”? 

What are availability zones?  

RDS 

What are they? Why are they useful? 

Have a general idea of to spin up and connect to an RDS 

 