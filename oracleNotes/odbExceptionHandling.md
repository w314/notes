# PL/SQL Exception Handling

## Propagation of Exceptions

An exception occuring in an inner block:
- is handled by inner block exception handler if there is one
    - in this case inner block terminates normally
    - control resumed to outer block
- in lack of proper exception handler:
    - exception get propageted to successive outer blocks
    - until it gets handled
    - if none of the outer block handles it it propagetes to the calling evironment


## Handling predefined exceptions

### Predefined Exception

- are predefined in Oracle server with
    - error code
    - exception name
- are raised implicitly (automatically) by Oracle server
- handled by using the exception name

#### Types of Predefined Exceptions

- `NO_DATA_FOUND`
    - ORA-1403
    - SELECT statement matches no rows
- `TOO_MANY_ROWS`
    - ORA-1422
    - SELECT statement matches more than 1 row
- `DUP_VAL_ON_INDEX`
    - ORA-0001
    - UNIQUE constraints is violatelld
- `ZERO_DIVIDE`
    - ORA-1476
    - division by zero
- `VALUE_ERROR`
    - ORA-6502
    - possible errors:
        - arithmetic
        - conversion
        - truncation
        - size-constraint
- `INVALID_NUMBER`
    - ORA-1722
    - trying to convert character string to number


### Handling Predefined Exception

- use `WHEN` clause
- followed by exception name

```sql
DECLARE
BEGIN
  -- Values of employee with id 21 are retrieved and stored in the variables
  -- Exception handling section
  -- Pay attention it is singular EXCEPTION (not exceptions)
EXCEPTION
WHEN NO_DATA_FOUND THEN
  DBMS_OUTPUT.PUT_LINE ( 'Employee with ID '||v_employee_id||' is not present.');
END;
```

## `WHEN OTHERS THEN`

- handles all exceptions
    - predefined
    - non-predefined
    - user defined
- should be the last clause
- should be placed in the outermost block
- only one per block

```sql
DECLARE
BEGIN
EXCEPTION
WHEN TOO_MANY_ROWS THEN
  DBMS_OUTPUT.put_line ('Too many rows are fetched');
WHEN OTHERS THEN
  DBMS_OUTPUT.PUT_LINE ('Something went wrong!!');
  DBMS_OUTPUT.PUT_LINE ('Error Code: ' || SQLCODE);
  DBMS_OUTPUT.PUT_LINE ('Error Message: ' || SQLERRM);
END;
```
- `SQLCODE` function returns the error code
- `SQLERRM` function returns the error message

## User Defined Exceptions

- declare user defined exception as type `EXCEPTION`
    - `v_exc_name EXCEPTION;`
- raise user defined exception with 
    - `RAISE v_exc_name;`
- handle exception with:
    - `WHEN v_exc_name THEN`

Employee with the employee ID 105 wants to know whether he/she is eligible for home loan. An employee is eligible for home loan only if his/her salary is greater than or equal to 8000. If not eligible, raise an exception and handle with appropriate message.

```sql
DECLARE
  v_employee_id employees.employee_id%TYPE := 105;
  v_salary employees.salary%TYPE;
  e_home_loan_eligibility EXCEPTION;
BEGIN
  SELECT salary INTO v_salary FROM employees WHERE employee_id = v_employee_id;
  IF v_salary < 8000 THEN
    RAISE e_home_loan_eligibility;
  END IF;
  DBMS_OUTPUT.PUT_LINE ('Employee with id '|| v_employee_id ||' is eligible for home loan');
EXCEPTION
WHEN e_home_loan_eligibility THEN
  DBMS_OUTPUT.PUT_LINE ('Employee with id '|| v_employee_id ||' is not eligible for home loan');
WHEN OTHERS THEN
  DBMS_OUTPUT.PUT_LINE ('Something went wrong!!');
  DBMS_OUTPUT.PUT_LINE ('Error Code: ' || SQLCODE);
  DBMS_OUTPUT.PUT_LINE ('Error Message: ' || SQLERRM);
END;
```

## The `PRAGMA EXCEPTION_INIT` Declarative
> Tells the compliler to sssociate user-defined exception name with an Oracle error number.

### `pragma`
> Compiler directive that is processed at compile time not runtime.


Syntax:

`PRAGMA EXCEPTION_INIT(exception_name, -Oracle_error_number);`
- `-Oracle_error_number` is the negative value of the error code
- must be after the user-defined exception in the same declarative section
- scope of `PRAGMA EXCEPTION_INIT` is only within the program.
- you can use it with predefined exceptions as welll

### Non-Predefined Exception
- Oracle server errors without an exception name in PL/SQL
- their error code can be assigned to an exception name with `PRAGMA EXCEPTION_INIT`
- they are raised automatically by Oracle server


### Example
```sql
DECLARE
  v_job_id jobs.job_id%TYPE       := 'ST_MAN';
  -- declare user-defined exception
  e_integrity_constraint EXCEPTION;
  -- assosicate user-defined exception name to Oracle error number  
  PRAGMA EXCEPTION_INIT (e_integrity_constraint, -02292 );
BEGIN
  --deleting the given job
  DELETE FROM jobs WHERE job_id=v_job_id;
  --handling of exceptions
EXCEPTION
WHEN e_integrity_constraint THEN
  DBMS_OUTPUT.PUT_LINE ('Cannot delete job with job id '||v_job_id||' as employees are assigned to it');
WHEN OTHERS THEN
  DBMS_OUTPUT.PUT_LINE ('Something went wrong!!');
  DBMS_OUTPUT.PUT_LINE ('Error Code: ' || SQLCODE);
  DBMS_OUTPUT.PUT_LINE ('Error Message: ' || SQLERRM);
END;
```

## `RAISE_APPLICATION_ERROR`

Used to raise user-defined exception with an error number and error message.
- `RAISE_APPLICATION_ERROR(error_number, error_message)`
- error_number can range from -20000 to -29999
- error message can max 512 characters
- can be used in code's:  
    - executable part
    - exception handling part
- can be handled with `WHEN OTHERS THEN`
- is implicitelly rolled back if not handled


Example:

```sql
DECLARE
  v_employee_id employees.employee_id%TYPE := 105;
  v_salary employees.salary%TYPE;
BEGIN
  SELECT salary INTO v_salary FROM employees WHERE employee_id = v_employee_id;
  IF v_salary < 8000 THEN
    RAISE_application_error(-20001,'Employee with id '|| v_employee_id ||' is not eligible for home loan');
  END IF;
  DBMS_OUTPUT.PUT_LINE ('Employee with id '|| v_employee_id ||' is eligible for home loan');
EXCEPTION
WHEN OTHERS THEN
  DBMS_OUTPUT.PUT_LINE ('Something went wrong!!');
  DBMS_OUTPUT.PUT_LINE ('Error Code: ' || SQLCODE);
  DBMS_OUTPUT.PUT_LINE ('Error Message: ' || SQLERRM);
END;
```

## Error Logging

### Create Table for Loggin Errors

```sql
CREATE TABLE error_log
  (
    error_code    INTEGER,
    error_message VARCHAR2 (250),
    occured_at    TIMESTAMP,
    comments      VARCHAR2 (250)
  );
```

### Log Errors

Example
```sql
DECLARE
    v_employee_id employees.employee_id%type := 21;
    v_first_name employees.first_name%TYPE;
    v_phone_number employees.phone_number%TYPE;
    v_error_code INTEGER;
    v_error_msg VARCHAR2 (4000);
    v_comment VARCHAR2 (4000);
BEGIN
    --Values of employee with id 21 are retrieved and stored in the variables
    SELECT first_name,phone_number 
        INTO v_first_name,v_phone_number 
        FROM employees 
        WHERE employee_id = v_employee_id;
    DBMS_OUTPUT.PUT_LINE ('Employee ID: ' || v_employee_id);
    DBMS_OUTPUT.PUT_LINE ('First Name: ' || v_first_name);
    DBMS_OUTPUT.PUT_LINE ('Contact Number: ' || v_phone_number);
--Handling of exceptions
EXCEPTION
WHEN TOO_MANY_ROWS THEN
    --Assigning the values of SQLCODE, SQLERRM and comments to variables
    v_error_code:=SQLCODE;
    v_error_msg :=SQLERRM;
    v_comment:='Requirement 2: Query is returning more than one record';
    --Inserting the error information
    INSERT INTO error_log
        (error_code,error_message,occured_at,comments)
        VALUES
        (v_error_code,v_error_msg,systimestamp,v_comment);
WHEN OTHERS THEN
    --Assigning the values of SQLCODE, SQLERRM and comments to variables
    v_error_code:=SQLCODE;
    v_error_msg :=SQLERRM;
    v_comment :='Requirement 2: Some error occured';
    --Inserting the error information
    INSERT INTO error_log
        (error_code,error_message,occured_at,comments)
        VALUES 
        (v_error_code,v_error_msg,systimestamp,v_comment);
END;
```