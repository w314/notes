pl-sql, trigger

# Req-44: Check experience of every employee before changing his job
Employee needs to have at least 2 years of experience in company for his job to be changed. If not, raise a exception with message 'Experience is not sufficient'

However if employee job is 'FI_MGR' or 'AD_PRES', this requirement need not be met.

Develop a trigger to check this before modifying job of every employee.

## Trigger

```sql
CREATE OR REPLACE TRIGGER trg_check_emp_experience
    EFORE UPDATE OF job_id ON employees
    FOR EACH ROW
        WHEN(OLD.job_id <> 'FI_MGR' OR OLD.job_id <>'AD_PRES')
BEGIN
    IF SYSDATE - :OLD.hire_date < 2 * 365 THEN
        RAISE_APPLICATION_ERROR(-20002, 'Experience not sufficient');
    END IF;
END;
```