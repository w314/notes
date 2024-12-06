
## Req-6 Add new job

HR Manager wants to add a new job Advertising Director (ADV_DIR).

VERSION A
- develop a STORED PROCEDURE program to add new job
- add it to the database only if the same job ID does not exist, else display the message "ADV_DIR already exists"
- use it with
    - Advertising Director, 
    - ADV_DIR 
    - minimum salary as 5000 
    - maximum salary and 10000


VERSION B
- use (not stored procedure) anonymus block where
- Do not provide job name and handle ORA-01400 error for null value violation

### VERSION A

#### Stored Procedure

```sql
CREATE OR REPLACE PROCEDURE sp_add_job(
    p_job_id IN jobs.job_id%TYPE,
    p_job_title IN jobs.job_title%TYPE,
    p_min_salary IN jobs.max_salary%TYPE,
    p_max_salary IN jobs.max_salary%TYPE,
    p_status OUT NUMBER)
IS
    v_job_id_count NUMBER(2);
BEGIN
    -- check for valid job ID
    SELECT COUNT(job_id) INTO v_job_id_count
        FROM jobs WHERE job_id = p_job_id;
    IF v_job_id_count > 0 THEN
        p_status := -1;
    ELSE
        INSERT INTO jobs 
            (job_id, job_title, min_salary, max_salary)
            VALUES 
            (p_job_id, p_job_title, p_min_salary, p_max_salary);
        p_status := 0;
    END IF;
    EXCEPTION
    WHEN OTHERS THEN
        p_status := -2;
END;
```

#### Use Store Procedure

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_job_id jobs.job_id%TYPE := 'ADV_DIR';
    v_job_title jobs.job_title%TYPE := 'Advertising Director';
    v_min_salary jobs.max_salary%TYPE;
    v_max_salary jobs.max_salary%TYPE := 10000;
    v_status NUMBER(1);
BEGIN
    sp_add_job(v_job_id, v_job_title, v_min_salary, v_max_salary, v_status);
    IF v_status = 0 THEN
        DBMS_OUTPUT.PUT_LINE('Job successfully added');
    ELSIF v_status = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Job id ' || v_job_id  || ' is invalid.');
    ELSIF v_status = -2 THEN
        DBMS_OUTPUT.PUT_LINE('Some other error occured');
    END IF;
    EXCEPTION
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