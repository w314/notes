createdAt: "2020-01-27T17:17:43.946Z"
updatedAt: "2020-02-07T20:09:26.848Z"
type: "MARKDOWN_NOTE"
folder: "e6d3330423734e2f4fd6"
title: "EC2 (Elastic Cloud Computer) and PVC (Private Virtual Cloud) in AWS"
tags: [
  "aws"
  "ec2"
  "pvc"
  "ebs"
]
content: '''
  ## `EC2` (Elastic Cloud Computer) and `PVC` (Private Virtual Cloud) in AWS
  
  ### Setup your `VPC` Virtual Private Cloud
  
  - On AWS Management Console enter `VPC` in the `Find Services` box
  - Click `Launch VPC Wizard` button
  - Select `VPC with a Single Public Subnet`
  - add `VPC Name`
  - Select first AZ from `Availability Zone`
  - Leave everything else as default
  - Click `Create VPC` button
  - When you see that you VPC was succesfully created click the `OK` button down right
  
  ### Launch a `EC2` Elastic Cloud Compute instance
  - Find `EC2` by serching for it
  - On `EC2` console click on `Instances` on the left
  - Click `Launch Instance`
  - Select `Amazon Linux 2 AMI (HVM), SSD Volume Type` Amazon Machine Image
  - For `Intance Type` select `free tier eligible` `t2.micro`
  - Click `Next: Configure Instance Details`
  - Enter 1 for `Number of instances`
  - For `Network` select `VPC` created before
  - Select subnet (there was only 1 choice)
  - Leave everything as default
  
  
  ### Attach `EBS` (Elastic Block Store) volume
  - Click on `Next: Add Storage` on the bottom of page
  - The next step will show that there is already a `root` volume attached to your instance - this is an EBS volume. To add additional storage click on `Add New Volume`
  - Select `Delete on Termination`
  - Click `Review and Launch`
  - Click `Launch`
  - Select `Create a new key pair`
  - Name you pair
  - Click `Download Key Pair`
  - Click `Launch Instances`
  
  ### Check you new instance
  - On your `EC2 Dashboard` you can see you instance running in the `Instances` tab
  
  ### Delete `EC2` and `PVC`
  - On the `EC2 Dashboard` Select your `EC2 Instance` and click `Actions` -> `Instance State` -> `Termintate`
  - On the `VPC Dashboard` select the `VPC` just created and click `Actions` -> `Delete VPC`
  
  ### Setup `EC2 Auto Scaling`
  
  
  ### User `EC2 Load Balancing`
  - Make sure your `EC2` instances are up and running
  - Navigate to `EC2 Dashboard`
  - Find `Load Balancing` in the left panel, click `Load Balancers`
  - 
  
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
