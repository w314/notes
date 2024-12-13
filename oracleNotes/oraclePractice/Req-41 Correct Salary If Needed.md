pl-sql, oracle, sql, trigger, triggering constraint

# Req-41:  Employee salary should be in the range of minimum and maximum salary of his job
- Every employee salary should be greater than or equal to the minimum salary of his job. 
- Before adding any employee this requirement has to be checked. 
- WHen updateing employee salary this requirement has to be checked.
- If the salary is less than the minimum salary, then employee's salary should be inserted with the minimum salary of his job.
- If salary is greater than maximum salary then raise an exception with message 'Employee salary cannot be more than max salary of his job'.
- However, if that employee is PRESIDENT (JOB_ID is 'AD_PRES') of the company then salary need not be greater than the minimum salary
- Develop a trigger to check if salary is valid or not before adding every employee or changing the salary of any employee.

## Trigger

```sql
CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT OR UPDATE OF salary ON employees
FOR EACH ROW
    -- adding trigger constraint
    -- jobs with id AD_PRES won't be affected by trigger
    -- NOT no need for ':' before NEW
    WHEN(NEW.job_id <> 'AD_PRES')
DECLARE
    v_min_salary jobs.min_salary%TYPE;
    v_max_salary jobs.max_salary%TYPE;
BEGIN   
    SELECT min_salary, max_salary INTO v_min_salary, v_max_salary
        FROM jobs WHERE job_id = :new.job_id;
    IF :new.salary < v_min_salary THEN
        :new.salary := v_min_salary;
        RETURN;
    END IF;
    IF :new.salary > v_max_salary THEN
        RAISE_APPLICATION_ERROR(-20001, 'Employee salary cannot be more than max salary of his job');
    END IF;
END;
```