pl-sql, block, record, log, error handling
## Req-2 View phone number of employees by first name

- employee wants to view the employee ID, first name, last name, department name and phone number of other employees.  
- create a record type to store only these values of an employee.
Retrieve and display the phone number of employee with first name 'John' and 
- display appropriate message if there no employee with the given first name 
- or if there are more than one employee with the given first name.
- ALSO LOG all exceptions raised.
- invoke the function from anonymous block for employee ID 110 and 119.




## Create Log Table

Create table for log:
```sql
CREATE TABLE error_log (
    error_code NUMBER(5),
    error_message VARCHAR2(250),
    occured_at TIMESTAMP,
    comments VARCHAR2(250)
);
```


## Get Phone Number

```sql
SET SERVEROUTPUT ON;

DECLARE
    -- declare RECORD TYPE
    TYPE type_emp_detail IS RECORD
    (
        phone_number employees.phone_number%TYPE
        -- other fields would be here
        -- with ',' at the end of each line except the last one
    );
    -- declare RECORD of TYPE
    rec_emp_detail type_emp_detail;
    v_first_name employees.first_name%TYPE := 'Peter';
    -- for logging errors
    v_error_code error_log.error_code%TYPE;
    v_error_message error_log.error_message%TYPE;
    v_comment error_log.comments%TYPE;
BEGIN
    SELECT phone_number
        INTO  rec_emp_detail
        FROM EMPLOYEES
        WHERE first_name = v_first_name;
    DBMS_OUTPUT.PUT_LINE('First Name: ' || v_first_name);
    -- access field of record
    DBMS_OUTPUT.PUT_LINE('Phone Number: ' || rec_emp_detail.phone_number);
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Employee : ' || v_first_name || ' does not exists.');
        -- it is not allowed ot use SQLCODE or SQLERRM in the INSERT statement
        v_error_code := SQLCODE;
        v_error_message := SQLERRM;
        v_comment := 'Requirement 1 - Employee ID does not exist.';
        INSERT INTO error_log
            (error_code, error_message, occured_at, comments)
            VALUES
            (v_error_code, v_error_message, SYSTIMESTAMP, v_comment);
    WHEN TOO_MANY_ROWS THEN
        DBMS_OUTPUT.PUT_LINE('There is more than 1 employee with the name ' || v_first_name);
        v_error_code := SQLCODE;
        v_error_message := SQLERRM;
        v_comment := 'Too many rows returned';
        INSERT INTO error_log
            (error_code, error_message, occured_at, comments)
            VALUES
            (v_error_code, v_error_message, SYSTIMESTAMP, v_comment);
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong!');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
        v_error_code := SQLCODE;
        v_error_message := SQLERRM;
        v_comment := 'Other error.';
        INSERT INTO error_log
            (error_code, error_message, occured_at, comments)
            VALUES
            (v_error_code, v_error_message, SYSTIMESTAMP, v_comment);
END;
```