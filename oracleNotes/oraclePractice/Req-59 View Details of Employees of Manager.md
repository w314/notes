pl-sql, cursor, record

# Req-59: Manager wants to view specific details of employees reporting to him
Manager of marketing department, department ID 50, wants to view employee ID, salary and hire_date of employees reporting to him.  

VERSION 1
- use Cursor %ROWTYPE in SQL Developer:

VERSION 2
- View only employee ID, salary and hire_date of employees. 
- create appropriate record

## Version 1

```sql
SET SERVEROUTPUT ON;

DECLARE 
    CURSOR cur_emp_in_dept(p_department_id employees.department_id%TYPE)
    IS SELECT * FROM employees WHERE department_id = p_department_id;
    v_department_id employees.department_id%TYPE;
    rec_emp_details cur_emp_in_dept%ROWTYPE;
BEGIN
    v_department_id := 50;
    OPEN cur_emp_in_dept(v_department_id);
    LOOP
        FETCH cur_emp_in_dept INTO rec_emp_details;
        EXIT
    WHEN cur_emp_in_dept%NOTFOUND;
    DBMS_OUTPUT.PUT_LINE('First Name ' || rec_emp_details.first_name);
    DBMS_OUTPUT.PUT_LINE('Job ID ' || rec_emp_details.job_id);
    END LOOP;
END;
```

## Version 2

```sql
SET SERVEROUTPUT ON;

DECLARE 
    CURSOR cur_emp_in_dept(p_department_id departments.department_id%TYPE)
    IS SELECT employee_id, salary, hire_date
        FROM employees WHERE department_id = p_department_id;
    TYPE type_emp_detail IS RECORD
    (
        employee_id employees.employee_id%TYPE,
        salary employees.salary%TYPE,
        hire_date employees.hire_date%TYPE
    );
    rec_emp_details type_emp_detail;
    v_department_id employees.department_id%TYPE;
BEGIN
    v_department_id := 50;
    OPEN cur_emp_in_dept(v_department_id);
    LOOP
        FETCH cur_emp_in_dept INTO rec_emp_details;
    EXIT
        WHEN cur_emp_in_dept%NOTFOUND;    
    DBMS_OUTPUT.PUT_LINE('==============================================');
    DBMS_OUTPUT.PUT_LINE('Employee ID: ' || rec_emp_details.employee_id);
    DBMS_OUTPUT.PUT_LINE('Salary: ' || rec_emp_details.salary);
    DBMS_OUTPUT.PUT_LINE('Hire Date: ' || rec_emp_details.hire_date);
    END LOOP;
END;
```