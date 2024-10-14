mysql, cvs, import, sql

# How Import CVS File to MySql

To find out the folder that files can be uploaded from run:
```sql
SELECT @@secure_file_priv;
```

Load data with:
```sql
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 9.0/Uploads/flag.csv' 
INTO TABLE flag 
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```