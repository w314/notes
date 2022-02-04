createdAt: "2020-01-31T17:18:24.443Z"
updatedAt: "2020-02-07T20:09:35.538Z"
type: "MARKDOWN_NOTE"
folder: "e6d3330423734e2f4fd6"
title: "AWS Static Website Hosting"
tags: [
  "aws"
  "hosting"
  "static_website"
  "s3"
  "iam"
  "cloudfront"
]
content: '''
  # AWS Static Website Hosting
  
  ## Create `S3` bucket to hold website files
  - Navigate to `S3`
  - Click `Create bucket`
  - Enter `Bucket name` (must be globally unique)
  - Click `Next` -> `Next` to get to `Set Permissions`
  - Unclick `Block all public access`, you need public access to host your static website
  - Click `Next` -> `Create bucket`
  
  ## Upload files to the `S3` bucket created
  
  ## Secure bucket via `IAM`
  - Open bucket
  - Click on `Permissions` tab
  - Click on `Bucket Policy` and enter:
  ```JSON
  {
    "Version":"2012-10-17",
    "Statement":[
      {
        "Sid":"AddPerm",
        "Effect":"Allow",
        "Principal": "*",
        "Action":["s3:GetObject"],
        "Resource":["arn:aws:s3:::your-website/*"]
      }
    ]
  }
  ```
  - Replace `your-website` with the name of you bucket
  - Click `Save`
  - Ignore warning that 'This bucket has public access', you need public access to host your static website
  
  ## Configure `S3` bucket for `Static website hosting`
  - Open bucket
  - Click on `Properties`
  - Click on `Static website hosting`
  - Select `Use this bucket to host a website`
  - For both `Index document` and `Error document` enter index.html
  - Click `Save`
  
  ## Distribute website via `CloudFront`
  - Navigate to `CloudFront`
  - Click `Create Distribution`
  - For `Select a delivery method for your content` click `Get Started` under `Web`
  - Under `Origin Settings`
    - Under `Origin Domain Name` select the bucket you have created
    - Under `Origin Path`, enter `/` to indicate the root level (It doens't actually accept it, it looks like it treats it as default)
  - Leave all else as default
  - Click `Create Distribution` at the bottom of the page (may take 10 minutes)
  
  
  
  
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
