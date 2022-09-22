createdAt: "2019-08-27T18:12:08.789Z"
updatedAt: "2020-02-07T20:13:35.954Z"
type: "MARKDOWN_NOTE"
folder: "1b2c017ab342eea0830f"
title: "Using multiple tables in sql"
tags: [
  "sql"
  "join"
]
content: '''
  # Using multiple tables in sql
  
  ## Using sub_squeries in the `WHERE` clause
  ```sql
  SELECT *
  FROM employees
  WHERE department_id IN
    (SELECT department_id
     FROM departments 
     WHERE location = 'location1')
  ```
  
  ## Specifying several tables in the `FROM` clause
  
  - full or cartesian join when every row of the first table is joined with every row of the second table
  
  ```sql
  SELECT *
  FROM employees, departments
  ```
  
  - additional operands would limit the result set
  
  ```sql
  SELECT *
  FROM employees, departments
  WHERE epoyees.department_id = departments.department_id
  ```
  - by using aliases for table names, even as prefix:
  ```sql
  SELECT E.name, D.name
  FROM employees E, departments D
  WHERE E.department_id = D.department_id;
  ```
'''
linesHighlighted: []
isStarred: false
isTrashed: false
