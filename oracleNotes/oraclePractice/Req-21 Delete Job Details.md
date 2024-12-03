# Req-21 Delete Job Details

HR Manager wants to delete job details with job ID 'ST_MAN'.
Handle inegrity constraint exception with user defined exception.

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_job_id jobs.job_id%TYPE := 'ST_MAN';
    e_integrity_constraint EXCEPTION;
    PRAGMA EXCEPTION_INIT(e_integrity_constraint, -2292);
BEGIN   
    DELETE FROM jobs WHERE job_id = v_job_id;
    EXCEPTION
    WHEN e_integrity_constraint THEN
        DBMS_OUTPUT.PUT_LINE('Cannot delet job with id ' || v_job_id || ' there are employees assigned to it');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE ('Something went wrong!!');
        DBMS_OUTPUT.PUT_LINE ('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE ('Error Message: ' || SQLERRM);
END;
```