pl-sql, cursor

# Req-48: HR List the details of all the employees who report to a manager
HR manager wants to view all details of all the employees who report to a specific manager.

VERSION 1
- pass manager id(103) as parameter 

VERSION 2
- use cursor for loop

VERSION 3
- declare cursor within for loop

## Version 1

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

## Version 2

```sql
SET SERVEROUTPUT ON;

DECLARE
    CURSOR cur_emp(p_manager_id employees.manager_id%TYPE)
    IS SELECT * FROM employees WHERE manager_id = p_manager_id;
    v_curr_man_id employees.manager_id%TYPE;
BEGIN
    v_curr_man_id := 103;
    FOR rec_emp IN cur_emp(v_curr_man_id)
    LOOP
        DBMS_OUTPUT.PUT_LINE(rec_emp.employee_id || ' - ' || rec_emp.first_name);
    END LOOP;
    EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error');
END;
```


## Version 3

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_manager_id employees.manager_id%TYPE := 103;
BEGIN
    -- declare cursor within FOR loop
    FOR rec_emp IN (SELECT * FROM employees WHERE manager_id = v_manager_id)
    LOOP
        DBMS_OUTPUT.PUT_LINE(rec_emp.employee_id || ' - ' 
            || rec_emp.hire_date || ' - '  || rec_emp.salary);
    END LOOP;
    EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error');
END;
```