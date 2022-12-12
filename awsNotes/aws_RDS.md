createdAt: "2020-01-29T01:07:08.140Z"
updatedAt: "2020-02-07T20:09:49.847Z"
type: "MARKDOWN_NOTE"
folder: "e6d3330423734e2f4fd6"
title: "RDS (Relational Database Service) in Amazon Web Services (AWS)"
tags: [
  "aws"
  "rds"
  "mysql"
]
content: '''
  ## `RDS` (Relational Database Service) in Amazon Web Services (AWS) 
  
  ### Setup a `MySQL` database in `AWS`
  - Find `RDS` on `Management Console`
  - On the left hand side click `Databases`
  - Click `Create Database` in upper right corner
  - Select `MySql` under `Engine Options`
  - Under `Templates` select `Free tier`
  - Enter name under `DB instance identifier` (This will NOT be the name of the database)
  - Enter `Mater username`
  - Enter `Master password`
  - Under `Virtual Private Cloud (VPC)` select `Create new`
  - Under `Connectivity` open `Additional connectivity configuration`
  - Make sure `Subnet group` is `Create new DB Subnet Group`
  - Leave the following settings as default:
      - `Subnet group`
      - `Public accessible`
      - `Availability Zone`
      - `VPC security group`
  - Open `Additional Configuration`
  - Under `Database options` enter `Initial database name` and leave rest as default
  - Under `Deletion Protection` make sure `Enable deletion protection` is unchecked (For learning purposes, **in real production you would want it checked**)
  - Click `Create database`
  
  ## View database instance
  - Open you database by selecting and double clicking on it
  - Make sure in the `Summary` tab `Info` shows `Available`
  
  ### Delete database instance
  - In `RDS` Dashboard select `Databases` on the left panel
  - Select your databases's radio button
  - Click `Actions` -> `Delete`
  - Uncheck `Create final snapshot`
  - Check `I acknowledge that upon instance deletion, automated backups, including system snapshots and point-in-time recovery, will no longer be available`
  - Confirm deletion as asked
  - Click `Delete` 
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
