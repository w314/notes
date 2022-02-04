createdAt: "2020-02-21T20:30:13.173Z"
updatedAt: "2020-02-21T21:24:45.144Z"
type: "MARKDOWN_NOTE"
folder: "0502aa55141f2315e808"
title: "Postbird to connect to our AWS RDS"
tags: [
  "postbird"
  "aws"
  "rds"
]
content: '''
  # `Postbird` to connect to our `AWS` `RDS`
  
  `Postbird` is a `postgreSQL` GUI client.
  ## Create database
  - Create `PostgreSQL` database in `AWS`
  - Accept default `VPC`
  - After database is created configure it's `VPC`
    - Open database
    - click on its `VPC Security Group`
    - Edit `Inbound` to include
      - `Type`: `PostgreSQL`
      - `Protocol`: `TCP`
      - `Port Range`: 5432
      (selecting `PostgreSQL` as `Type` sets, `Protocol` and `Port Range`)
      - To allow public access to the database, change `Source` to `Anywhere`
      - Click `Save`
      
  ## Connect to database
  - Get your `endpoint` end `port` from your `aws` `rds` `Connectivity & security` information
  - Open [Postbird](http`s://www.electronjs.org/apps/postbird)
    - For `Host` and `Port` enter your `aws` `endpoint` and port
     - Enter `Username`, `Password`, `Database`
    - Click `Test Connection`
  - To store this connection in `Postbird` click `Save & Connect`
  - Create tables with the green `+` button in the lower left corner
  - 
'''
linesHighlighted: []
isStarred: false
isTrashed: false
