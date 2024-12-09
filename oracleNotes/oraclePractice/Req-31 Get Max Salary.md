# Req-31: Get the maximum salary of a particular job
Develop a stored function sf_get_max_salary 
- which accepts job_id as parameter and 
- returns the maximum salary for that job_id. 
- In case of invalid job_id, function returns -1 and 
- for any other error, returns -2
- Invoke the function with job_id as 'FI_MGR' and 'AD_PRE'.


## Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_max_salary(
    p_job_id jobs.job_id%TYPE)
    RETURN NUMBER
IS
    v_max_salary jobs.max_salary%TYPE;
BEGIN
    SELECT max_salary into v_max_salary
        FROM jobs WHERE job_id = p_job_id;
    RETURN v_max_salary;
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        RETURN -1;
    WHEN OTHERS THEN
        RETURN -2;
END;
```

## Invoking stored function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_job_id jobs.job_id%TYPE := 'AD_PRE';
    v_max_salary jobs.max_salary%TYPE;
BEGIN
    v_max_salary := sf_max_salary(v_job_id);
    IF v_max_salary >= 0 THEN
        DBMS_OUTPUT.PUT_LINE('Max salary for job ' || v_job_id || ' is ' || v_max_salary);
    ELSIF v_max_salary = -1 THEN
        DBMS_OUTPUT.PUT_LINE('There is no job with id ' || v_job_id);
    ELSIF v_max_salary = -2 THEN
        DBMS_OUTPUT.PUT_LINE('Some error happened while retrieving max salary');
    END IF;
END;
```

