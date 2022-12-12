createdAt: "2020-01-29T19:23:32.537Z"
updatedAt: "2020-02-24T17:15:54.736Z"
type: "MARKDOWN_NOTE"
folder: "e6d3330423734e2f4fd6"
title: "S3 Bucket (Simple Storage Service) and CloudFront"
tags: [
  "aws"
  "s3"
  "cloudfront"
  "signed_url"
]
content: '''
  ## `S3 Bucket` (Simple Storage Service) and `CloudFront`
  
  ### Create `S3` Bucket
  - Navigate to `S3`
  - Click `Create Bucket`
  - Enter `Bucket name` (must be globally unique)
  - Click `Next`
  - Click `Default encryption` for encryption, select `AES-256`
  - Click `Next`
  - Leave `Block public access` selected
  - Click `Next`
  - Click `Create Bucket`
  
  ### Upload object to bucket
  - Doubleclick on bucket to open it
  - Click `Upload` button
  - Click `Add files`
  - Select file, click `Open`
  - Click `Upload`
  
  ### Set up bucket for `signed URL` connection capability
  - Open your bukcet
  - Click on `Permissions`
  - Click on `CORS configuration`
    - as default `S3` bucket doesn't allow requests from any domain
    - to allow that add a cors policy like below in the `CORS configuration editor`
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <CORSRule>
        <AllowedOrigin>*</AllowedOrigin>
        <AllowedMethod>POST</AllowedMethod>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedMethod>GET</AllowedMethod>
        <AllowedMethod>DELETE</AllowedMethod>
        <AllowedMethod>HEAD</AllowedMethod>
        <AllowedHeader>*</AllowedHeader>
    </CORSRule>
    </CORSConfiguration>
    ```
    - click `Save`
  
  ### Set up permissions for `S3 bucket`
  - Need to make sure that only authorized users and system can access our bucket
  - 
  
  ### Create `CloudFront` distribution
  - Navigate to `CloudFront`
  - Click `Create distribution`
  - Under `Web` `delivery method` click `Get Started`
  - Under `Origin Settings`
      - Under `Origin Domain Name` select the bucket you have just created
      - (Under `Origin Path` enter `/` to indicate root level) looks like is not needed
  - Leave rest as default
  - Click `Create Distribution` at the bottom of the page (it may take 10 minutes)
  
  ### Delete `CloudFront` Distribution
  - To delete a `CloudFront` distribution select the radio button next to the delivery method
  - Click `Disable` -> `Yes, Disable` -> `Close`
  - After disabled (can take upto 15 minutes), select the delivary method again
  - Click `Delete` -> `Yes, Delete`
  
  ### Delete `S3 Bucket`
  - Navigate to `S3`
  - Select radio button next to bucket to delete
  - Click `Delete`
  - Type name of bucket to confirm deletion
  - Click `Confirm` 
'''
linesHighlighted: []
isStarred: false
isTrashed: false
