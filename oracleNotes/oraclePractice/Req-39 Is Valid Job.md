# Req-39: Determine if a job title is a valid one

Develop a stored function sf_is_valid_job 
- that accepts job title and 
- returns true or false based on whether the job title is a valid one. 
- In case of exception, function will return Null.
- Invoke the function with job title as 'Accountant' and 'Clerk'.

## Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_is_valid_job(
    p_job_title jobs.job_title%TYPE)
    RETURN BOOLEAN
IS
    v_job_title jobs.job_title%TYPE;
BEGIN
    SELECT job_title INTO v_job_title
        FROM jobs WHERE job_title = p_job_title;
    RETURN TRUE;
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        RETURN FALSE;
    WHEN OTHERS THEN
        RETURN NULL;
END;
```


## Invoking Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_job_title jobs.job_title%TYPE := 'Accountant';
    v_valid_job_title BOOLEAN;
BEGIN
    v_valid_job_title := sf_is_valid_job(v_job_title);
    IF v_valid_job_title THEN
        DBMS_OUTPUT.PUT_LINE('Valid job title');
    ELSIF NOT v_valid_job_title THEN
        DBMS_OUTPUT.PUT_LINE('Invalid job title');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Error');
    END IF;
END;
```