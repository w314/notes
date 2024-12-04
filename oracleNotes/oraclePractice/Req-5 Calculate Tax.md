
## Req-5 Calculate Tax

- Develop a PL/SQL program to calculate and display the tax amount 
    - of Steven King, employee ID 100.
- Tax is computed based on the below rules:
    - salary >= 15000 -> 15%
    - salary >= 8000 -> 10%
    - below 8000 0%

- before calculating check if he/she is a valid employee, 
    - if not raise a user defined exception and handle it with an appropriate message



```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 99;
    v_salary employees.salary%TYPE;
    v_tax_rate NUMBER(2);
    v_tax_amount NUMBER(8.2);
    e_invalid_employee EXCEPTION;
    PRAGMA EXCEPTION_INIT(e_invalid_employee, 100);
BEGIN
    SELECT salary INTO v_salary
        FROM employees WHERE employee_id = v_employee_id;
    IF v_salary >= 15000 THEN
        v_tax_rate := 15;
    ELSIF v_salary >= 8000 THEN
        v_tax_rate := 10;
    ELSE
        v_tax_rate := 0;
    END IF;
    v_tax_amount := v_salary * v_tax_rate / 100;
    DBMS_OUTPUT.PUT_LINE('Employee ID: ' || v_employee_id);
    DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);
    DBMS_OUTPUT.PUT_LINE('Tax Rate: ' || v_tax_rate);
    DBMS_OUTPUT.PUT_LINE('Tax Amount: ' || v_tax_amount);
    EXCEPTION
    WHEN e_invalid_employee THEN
        DBMS_OUTPUT.PUT_LINE('Employee ID ' || v_employee_id || ' is invalid');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Other problem occured');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```
