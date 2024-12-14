pl-sql, trigger, trigger contraint

# Req-50  Check for modifying the minimum salary of Job IT_PROG
- Business Rule: Whenever minimum salary of any job is updated, the new minimum salary should be greater than the existing minimum salary of that job; 
- if not raise an exception with error number -20000 and error message "Minimum salary of the job should not be less than current minimum salary".
- this rule is not applicable if Job is 'AD_PRES'

Develop a trigger TRG_UPDATE_MIN_SALARY to check this, before modifying minimum salary of every job.


```sql
CREATE OR REPLACE TRIGGER trg_update_min_salary
    BEFORE UPDATE OF min_salary ON jobs
    FOR EACH ROW
    -- need OLD or NEW in constraint but not the : before them
    WHEN (NEW.job_id <> 'AD_PRES')
BEGIN
    IF :NEW.min_salary < :OLD.min_salary THEN
        RAISE_APPLICATION_ERROR(-20000, 'Minimum salary of the job should not be less than current minimum salary');
    END IF;
END;
```
 