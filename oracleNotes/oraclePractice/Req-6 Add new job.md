
## Req-6 Add new job

HR Manager wants to add a new job Advertising Director (ADV_DIR).

VERSION A
- develop a PL/SQL program to add new job
    - Advertising Director, 
    - ADV_DIR 
    - minimum salary as 5000 
    - maximum salary and 10000
- add it to the database only if the same job ID does not exist, else display the message "ADV_DIR already exists"

VERSION B
- Do not provide job name and handle ORA-01400 error for null value violation

### VERSION A

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_job_id jobs.job_id%TYPE := 'ADV_DIR';
    v_job_title jobs.job_title%TYPE := 'Advertising Director';
    v_min_salary jobs.max_salary%TYPE := 5000;
    v_max_salary jobs.max_salary%TYPE := 10000;
BEGIN
    INSERT INTO jobs 
        (job_id, job_title, min_salary, max_salary)
        VALUES (v_job_id, v_job_title, v_min_salary, v_max_salary);
    EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        DBMS_OUTPUT.PUT_LINE('ADV_DIR already exists');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong.');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```

### VERSION B
```sql
SET SERVEROUTPUT ON;

DECLARE
    v_job_id jobs.job_id%TYPE := 'ADV_DIR';
    v_min_salary jobs.max_salary%TYPE := 5000;
    v_max_salary jobs.max_salary%TYPE := 10000;
    e_null EXCEPTION;
    PRAGMA EXCEPTION_INIT(e_null, -1400);
BEGIN
    INSERT INTO jobs 
        (job_id, min_salary, max_salary)
        VALUES (v_job_id, v_min_salary, v_max_salary);
    EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        DBMS_OUTPUT.PUT_LINE('ADV_DIR already exists');
    WHEN e_null THEN
        DBMS_OUTPUT.PUT_LINE('Cannot insert NULL value to column with NOT NULL constraint');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong.');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```