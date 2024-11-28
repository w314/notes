# Oracle Cursor
> Used for multi-row processing.


## Implicit Cursor

A implicit cursor is opened by the database to process each SQL statement below that is not associated with an explicit cursor.
- SELECT
- INSERT
- UPDATE
- DELETE

The name of the  implicit cursor is `SQL`.

Implicit cursors have [attributes](https://docs.oracle.com/cd/B28359_01/appdev.111/b28370/sql_cursor.htm#LNPLS01348).


After the update statement is executed cursor will be closed.



## Explicit Cursor

Declare Cursor
- `CURSOR cursor_name IS <SELECT statement>`
- cursor is given a name
- cursor is associated with a query

Open Cursor
- `OPEN cursor_name;`
- PL/SQL raises no error in case of zero or only 1 row

Fetch Data With
- `FETCH <cursor_name> INTO PL/SQL variables;`
- cursor advances to the next row
- reads and stores the data

Close Cursor
- CLOSE cursor_name;`
- active set becomes undefined freeing its memory
- using cursor after it's closed raises `INVALID_CURSOR` exception
- it is possible to terminate PL/SQL block without closing the cursor, but it is bad practice


### Explicit Cursor Attributes

- `%ISOPEN`
    - boolean
    - evaluates if cursor is open
- `%NOTFOUND`
    - boolean
    - TRUE if the most recent FETCH does not return a row
- `%FOUND`
    - boolean
    - TRUE if the most recent FETCH returns a row
- `%ROWCOUNT`
    - number
    - gives total number of rows fetched so far

### Explicit Cursor Example

Requirement: HR manager wants to view the details (employee ID, salary and hire date) of all the employees working in Marketing department (department ID 20)

```sql
SET SERVEROUTPUT ON;

DECLARE
    -- declare cursor with a name
    CURSOR cur_emp_in_dept
    IS
        -- associate cursor with query
        SELECT employee_id, salary, hire_date
            FROM employees
            WHERE department_id = 20;
        -- declare variables to store data in
        v_emp_id employees.employee_id%TYPE;
        v_salary employees.salary%TYPE;
        v_hire_date employees.hire_date%TYPE;
BEGIN
    -- start processing queried rows
    OPEN cur_emp_in_dept;
        LOOP
            -- store current employee data
            FETCH cur_emp_in_dept INTO v_emp_id, v_salary, v_hire_date;
            -- define loop exit condition
            EXIT
                -- exit when no more employees to process
                WHEN cur_emp_in_dept%NOTFOUND;
            -- if %NOTFOUND is false
            -- output current employee details
            DBMS_OUTPUT.PUT_LINE('Employee ID: ' || v_emp_id);
            DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);
            DBMS_OUTPUT.PUT_LINE('Hire Date: ' || v_hire_date);
            DBMS_OUTPUT.PUT_LINE('_______________________________');
        END LOOP;
    CLOSE cur_emp_in_dept;
END;     
```

### Referncing variables in cursor query

If we want to do the same query for several departments:
```sql
DECLARE
    -- declare variable for cursor query
    v_dept_id employees.department_id%TYPE;
    -- declare cursor
    CURSOR cur_emp_in_dept
    IS
        -- select rows to process
        -- use variable in query
        SELECT employee_id, salary, hire_date
            FROM employees
            WHERE department_id = v_dept_id;
        -- declare variables to store data like before
BEGIN
    -- set department value
    v_dept_id := 20;
    -- open cursor, its select query is executed now
    -- using the department value we just set
    OPEN cur_emp_in_dept;
    -- rest of the block is the same
```    

If v_dept_id is set at declaration to 30, but set before open to 20, the value just set before open cursor will be used. 

### Explicit Cursor with Parameters

- cursor parameter allows us to reopen and close the same cursor with different datasets
    - passing different departmetn id-s for example
    - to process employees of those departments
- cursor parameter has type but does not need size
    
```sql
DECLARE
    -- declare cursor
    -- cursor parameter needs type, but size
    CURSOR cur_emp_in_dept(p_dept_id employees.department_id%TYPE)
    IS
        -- select rows to process
        -- use parameter in cursor query
        SELECT employee_id, salary, hire_date
            FROM employees
            WHERE department_id = p_dept_id;
        -- declare variables to store data in like before
BEGIN
    -- open cursor, its select query is executed now
    -- pass parameter value
    OPEN cur_emp_in_dept(30);
    -- rest of the block is the same
;
```

## Cursor For Loop

Cursor FOR Loop Implicitely:
- opens the cursor
- declares a record against the cursor
    - in `FOR rec_emp IN cur_emp_in_dept`
    - using `%ROWTYPE`
    - implicitly
- fetches each row into the record
- closes the loop if all records are fetched
- can be used with cursor parameters
    - `FOR rec_emp IN cur_emp_in_dept(p_dept_id)`
- you can use the cursor more then once in the same block passing different parameters

Listing employee detials of a department.

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_dept_id employees.department_id%TYPE;
    CURSOR cur_emp_in_dept
    IS  
        SELECT employee_id, salary, hire_date
            FROM employees
            WHERE department_id = v_dept_id;
BEGIN
    v_dept_id := 20;
    -- data is retrieved in a for loop
    FOR rec_emp IN cur_emp_in_dept
    LOOP
        -- output data from fields of the record
        DBMS_OUTPUT.PUT_LINE('Employee ID: ' || rec_emp.employee_id);
        DBMS_OUTPUT.PUT_LINE('Salary: ' || rec_emp.salary);
    END LOOP;
END;
```


### Declaring Cursor within FOR Loop

If you do not have to reuse the cursor within the code block you can delcare if within the for loop itself.

```sql
SET SERVEROUTPUT ON;
DECLARE
BEGIN
    FOR rec_emp IN (SELECT employee_id, salary
        FROM employees
        WHERE department_id = 100)
    LOOP
        DBMS_OUTPUT.PUT_LINE('Employee ID: ' || rec_emp.employee_id);
        DBMS_OUTPUT.PUT_LINE('Salary: ' || rec_emp.salary);
    END LOOP;
END;
```