pl-sql, oracle, trigger

# Req-52: Keep a track of an employee's previous Job details 

HR Manager wants to keep a track of an employee's previous Job details for auditing in the future. After modifying employee's job the previous job details in which he worked should be recorded in JOB_HISTORY table.

If any employee record already exists in JOB_HISTORY table then start_date will be the end_date of previous job. Else, start_date will be hire_date of employee.

- Table was already created

```sql
CREATE OR REPLACE TRIGGER trg_update_job_history
    AFTER UPDATE OF job_id ON employees
    FOR EACH ROW
DECLARE
    v_log_count NUMBER(2);
    v_start_date employees.hire_date%TYPE;
BEGIN   
    SELECT COUNT(job_id) INTO v_log_count
        FROM job_history 
        WHERE employee_id = :NEW.employee_id;
    IF v_log_count > 0 THEN
        SELECT end_date INTO v_start_date
            FROM job_history WHERE employee_id = :NEW.employee_id
            ORDER BY end_date DESC
            FETCH FIRST 1 ROW ONLY;
    ELSE
        v_start_date := :NEW.hire_date;
    END IF;
    INSERT INTO job_history
        (employee_id, start_date, job_id, department_id)
        VALUES
        (:NEW.employee_id, v_start_date, :NEW.job_id, :NEW.department_id);
END;
```