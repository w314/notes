cursor, pl-sql

# Req-47: View the details of all the employees working in a department
- show emmployee ID, salary and hire date
- of a specific department

VERSION 1:
- pass the department as a variable to the cursor
- use Marketing department with id 20

VERSION 2:
- use cursor parameters
- run it for both department with id 20 and 30
- see ALL details fo employees


## Version 1

```sql
SET SERVEROUTPUT ON;

DECLARE
    -- declare variablest the cursor uses 
    -- before declaring the cursor
    v_department_id departments.department_id%TYPE := 20;
    -- declare cursor
    CURSOR cur_emp_in_dept
    IS
        SELECT employee_id, hire_date, salary 
            FROM employees WHERE department_id = v_department_id;
    -- declare variables to hold employee information
    v_employee_id employees.employee_id%TYPE;
    v_hire_date employees.hire_date%TYPE;
    v_salary employees.salary%TYPE;
BEGIN
    -- can change value of variable before opening cursor
    -- v_department_id := 30 would be valid here
    -- open cursor
    OPEN cur_emp_in_dept;
    -- loop through rows
    LOOP
        -- fetch data into variables
        FETCH cur_emp_in_dept INTO v_employee_id, v_hire_date, v_salary;
        -- set exit condition
        EXIT
        WHEN cur_emp_in_dept%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE(v_employee_id || ' - ' 
            || v_hire_date || ' - ' 
            || v_salary);
    END LOOP;
    -- close cursor
    CLOSE cur_emp_in_dept;
END;
```

## Version 2

```sql
SET SERVEROUTPUT ON;

DECLARE
    -- declare cursor with parameter
    CURSOR cur_emp_in_dept(p_department_id departments.department_id%TYPE)
    IS
        SELECT *
            FROM employees WHERE department_id = p_department_id;
    -- variable to hold current departmetn to pass as parameter to cursor
    v_current_dept departments.department_id%TYPE;
     -- declare variables to hold employee information
     -- use %ROWTYPE of the CURSOR
    rec_employee cur_emp_in_dept%ROWTYPE;
BEGIN
    v_current_dept := 20;
    DBMS_OUTPUT.PUT_LINE('Department - ' || v_current_dept);
    -- open cursor and pass parameters
    OPEN cur_emp_in_dept(v_current_dept);
    -- loop through rows
    LOOP
        -- fetch data into variables
        FETCH cur_emp_in_dept INTO rec_employee;
        -- set exit condition
        EXIT
        WHEN cur_emp_in_dept%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE(rec_employee.employee_id || ' - ' 
            || rec_employee.hire_date || ' - ' 
            || rec_employee.salary);
    END LOOP;
    -- close cursor
    CLOSE cur_emp_in_dept;
    -- open cursor with using different parameter value;
     v_current_dept := 30;
    DBMS_OUTPUT.PUT_LINE('Department - ' || v_current_dept);
    OPEN cur_emp_in_dept(v_current_dept);
    -- loop through rows
    LOOP
        -- fetch data into variables
        FETCH cur_emp_in_dept INTO rec_employee;
        -- set exit condition
        EXIT
        WHEN cur_emp_in_dept%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE(rec_employee.employee_id || ' - ' 
            || rec_employee.hire_date || ' - ' 
            || rec_employee.salary);
    END LOOP;
    -- close cursor
    CLOSE cur_emp_in_dept;
    EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error');
END;
```