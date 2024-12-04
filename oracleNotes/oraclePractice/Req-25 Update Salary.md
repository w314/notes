# Req-25: update the salary of employee with the given salary

- update the salary of employee 
    - with employee ID 123 
    - to 5500 
- before updating check if the new salary is not less than current salary
    - VERSION A if it is less then raise a user defined exception and handle with an appropriate message.
    - VERSION B user RAISE_APPLICATION_ERROR

### Version A
```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.department_id%TYPE := 123;
    v_salary employees.salary%TYPE;
    v_new_salary v_salary%TYPE := 5000;
    e_new_salary_lower_than_current EXCEPTION;
BEGIN   
    SELECT salary INTO v_salary
        FROM employees WHERE employee_id = v_employee_id;
    IF v_new_salary < v_salary THEN
        RAISE e_new_salary_lower_than_current;
    END IF;
    UPDATE employees SET salary = v_new_salary
        WHERE employee_id = v_employee_id;
    DBMS_OUTPUT.PUT_LINE('Successfully update salary from ' || v_salary || 
        ' to ' || v_new_salary);
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('There is no employee with id: ' || v_employee_id);
    WHEN e_new_salary_lower_than_current THEN
        DBMS_OUTPUT.PUT_LINE('New salary: ' || v_new_salary || 
            ' cannot be lower than current salary: ' || v_salary);
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong.');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```

### Version B
```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.department_id%TYPE := 123;
    v_salary employees.salary%TYPE;
    v_new_salary v_salary%TYPE := 3000;
BEGIN   
    SELECT salary INTO v_salary
        FROM employees WHERE employee_id = v_employee_id;
    IF v_new_salary < v_salary THEN
        RAISE_APPLICATION_ERROR(-20001, 'New salary cannot be lower than current salary');
    END IF;
    UPDATE employees SET salary = v_new_salary
        WHERE employee_id = v_employee_id;
    DBMS_OUTPUT.PUT_LINE('Successfully update salary from ' || v_salary || 
        ' to ' || v_new_salary);
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('There is no employee with id: ' || v_employee_id);
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong.');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```