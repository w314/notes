createdAt: "2019-09-03T18:48:03.164Z"
updatedAt: "2020-08-05T21:20:02.994Z"
type: "MARKDOWN_NOTE"
folder: "0502aa55141f2315e808"
title: "Using Jupyter Notebook to Analyze IBM DB2 database"
tags: [
  "ibm"
  "jupyter"
  "python"
  "db2"
  "#"
]

createdAt: "2019-09-05T20:25:13.811Z"
updatedAt: "2020-03-25T21:08:12.889Z"
type: "MARKDOWN_NOTE"
folder: "0502aa55141f2315e808"
title: "Jupyter Notebook"
tags: [
  "jupyter"
  "shorcuts"
]
content: '''
  # [Jupyter Notebook](https://jupyter.org/)
  
  A web application that allows you to combine explanatory text, math equations, code, and visualizations all in a single document.
  
  Installed using [Anaconda Python/R Distribution - Free Download](https://www.anaconda.com/distribution/)
  
  
  
  
  # Jupyter Notebook Shortcuts
  
  `esc` to switch to command mode
  `enter` to switch to edit mode
  `shift + enter` to run code
  
  ### When in command mode
  
  `m` to turn cell to `markdown`
  `a` to insert a cell above
  `b` to insert a cell below
  `ctrl + enter` run all selected cells
  `shift + up` select cells above
'''
linesHighlighted: []
isStarred: false
isTrashed: false

content: '''
  # Using Jupyter Notebook to Analyze IBM DB2 database
  
  - Load ipython-sql extension
  
  ```python
  %load_ext slql
  ```
  
  - establish connection so the database
  ```python
  %sql ibm_db_sa:\\\\qpv73871:w1d7bjbs%40xgvb0qt@dashdb-txn-sbox-yp-dal09-03.services.dal.bluemix.net:50000\\BLUDB
  ```
  
  
'''
linesHighlighted: [
  0
  1
]
isStarred: false
isTrashed: false
