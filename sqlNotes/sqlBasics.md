createdAt: "2019-08-20T21:27:21.099Z"
updatedAt: "2020-02-07T20:13:22.857Z"
type: "MARKDOWN_NOTE"
folder: "1b2c017ab342eea0830f"
title: "Basic SQL Commands"
tags: [
  "sql"
]
content: '''
  # Basic SQL Commands
  
  - creating tables
  
  ```sql
  CREATE TABLE food 
    (food_id INTEGER PRIMARY_KEY NOT NULL,
     name VARCHAR(256) NOT NULL
    )
  ```
  
  - inserting rows 
  
  ```sql
  INSERT INTO food
  food_id, name
  VALUES
  ('1', 'tökfőzelék'),
  ('2', 'vadas');
  ```
  
  - updating rows
  ```sql
  UPDATE food
  SET name = 'babgulyás'
  WHERE food_id = 1;
  ```
  
  - delete row
  ```sql
  DELETE FROM food
  WHERE food_id = 1;
  ```
  
  
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
