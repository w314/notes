functions, sql, case, nvl, upper, lower, max, min, avg, sum, count, to_date, to_char, to_number

# SQL Functions
>Built in modules provided by the database, can be used to perform calculations on data.

ALL functions return a **single value**.

Types of functions:
- single row function
    - return a single row for each row of input
    - operates on single row
    - used in `SELECT`, `WHERE`, `ORDER BY` and `HAVING` clauses
- mulitple row functions
    - returns single row irrespective of number of input rows
    - operate on multiple row 
    - used in `SELECT`, `ORDER BY` and `HAVING` clauses
     

## Single Row Functions

### Numeric Functions

- ABS
- ROUND
- CEIL
- FLOOR


### Character Functions
- UPPER
- LOWER
- CONCAST
- LENGTH
- SUBSTR(value, startPos, length)
    - index starts with 1
    - last paramater is the lenght of the substring


### Conversion Functions
- TO_CHAR(value, format) - used to format dates and numbers
```sql
TO_CHAR(3467.45, '9,999.99')
-- returns 3,467.45
TO_CHAR('27-Jul-2024', 'MON') 
-- returns JUL
TO_CHAR('27-Jul-2024', 'Month')
-- returns July 
TO_CHAR('27-Jul-2024', 'Dy')
-- returns Sat 
TO_CHAR('27-Jul-2024', 'May') 
-- returns Saturday
```
- TO_DATE(value, format) - string -> date
    - format string has to be used if date string is not in default Oracle format
- TO_NUMBER - string -> number


```sql
-- only valid with format string
SELECT 'Jan-01-2014' date_string, TO_DATE('Jan-01-2014', 'Mon-DD-YYYY')  conv_format FROM MyTable;
```
- **no need** to use `AS` it is assumed if there is **no** `,`
- `Oracle` date format is `DD-Mon-YYYY`



### Date Functions
- SYSDATE
- SYSTIMESTAMP
- ADD_MONTH(date, n)
- MONTHS_BETWEEN(date1, date2) - exact, can be 2. 67



## Aggreagate Function
- `SUM`, `AVG` for numeric columns only
- `MIN`, `MAX`, `COUNT` operate on all data types
- all ignore `NULL` values except `COUNT(*)`

```sql
SELECT COUNT(DISTINCT name) FROM Employees;
```

NOT SURE IT IS CORRECT BELOW
What is the output?
```sql
-- Table T has a single column A with 4 values:
-- -100, NULL, 200, 300

SELECT MAX(A) from T WHERE A > 1000;
```
NULL


## Miscellaneous  Functions

- `USER` returns current user
- `NVL(val1, val2)` 
    - substitues val1 with val2 if val1 is `NULL`
    - val1 and val2 has to be the same data type


## `CASE` Statement

```sql
SELECT score
CASE Designation
    WHEN score >= 90 THEN 'A'
    WHEN score >= 80 OR score = 77 THEN 'B'
    ELSE 'F'
END AS grade
FROM students;
```


