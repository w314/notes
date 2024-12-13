pl-sql, cursor

# Req-48: HR List the details of all the employees who report to a manager
HR manager wants to view all details of all the employees who report to a specific manager.
- pass manager id(103) as parameter 


## Block

```sql
SET SERVEROUTPUT ON;

DECLARE
   
    CURSOR cur_emp(p_manager_id employees.manager_id%TYPE)
    IS SELECT * FROM employees WHERE manager_id = p_manager_id;
    rec_emp_info cur_emp%ROWTYPE;
    v_manager_id employees.manager_id%TYPE := 103;
BEGIN
    OPEN cur_emp(v_manager_id);
    LOOP
        FETCH cur_emp INTO rec_emp_info;
        EXIT
    WHEN cur_emp%NOTFOUND;
    DBMS_OUTPUT.PUT_LINE(rec_emp_info.employee_id || ' - ' || rec_emp_info.first_name);
    END LOOP;
    CLOSE cur_emp;
    EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error');
END;
```

