# Req-24: View job details
- Develop a PL/SQL program to retrieve and display the job details 
- with job ID 'MGR' 
- and appropriate message if the job ID is not present.
- try with MK_MAN for valid job_id

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_job_id jobs.job_id%TYPE := 'MGR';
    rec_job_details jobs%ROWTYPE;
BEGIN
    SELECT * INTO rec_job_details
        FROM jobs WHERE job_id = v_job_id;
    DBMS_OUTPUT.PUT_LINE('Job Title: ' || rec_job_details.job_title);
    DBMS_OUTPUT.PUT_LINE('Salary: ' || rec_job_details.min_salary || ' - ' 
        || rec_job_details.max_salary);
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('There is no job ID: ' || v_job_id);
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Some other error');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```