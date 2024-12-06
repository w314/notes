
## Req-5 Calculate Tax

- Develop a PL/SQL program to calculate and display the tax amount 
    - of Steven King, employee ID 100.
- create stored function to calculate tax
    - Tax is computed based on the below rules:
        - salary >= 15000 -> 15%
        - salary >= 8000 -> 10%
        - below 8000 0%

- before calculating check if he/she is a valid employee, 
    - if not raise a user defined exception and handle it with an appropriate message
- handle any other exception

### Stored Function to Calculate Tax
```sql
-- declare function with paramaters it takes
CREATE OR REPLACE FUNCTION sf_calculate_tax(
    p_employee_id employees.employee_id%TYPE)
    -- declare return type do NOT specify size
    RETURN NUMBER
IS 
    -- variables used for tax calculation
    v_salary employees.salary%TYPE;
    v_tax_rate NUMBER(2);
    v_tax_amount v_salary%TYPE;
BEGIN
    -- fetch salary of employee
    SELECT salary INTO v_salary
        FROM employees WHERE employee_id = p_employee_id;
    -- calculate tax rate
    IF v_salary >= 15000 THEN
        v_tax_rate := 15;
    ELSIF v_salary >= 8000 THEN
        v_tax_rate := 10;
    ELSE 
        v_tax_rate := 0;
    END IF;
    -- calculate tax amount
    v_tax_amount := v_salary * (v_tax_rate / 100);
    -- return tax amount
    RETURN v_tax_amount;
    -- handle error
    EXCEPTION
    WHEN OTHERS THEN
        RETURN -1;
END;
```

### Invoke Stored Function to Calculate Tax

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 99;
    v_emp_id_check v_employee_id%TYPE;
    v_tax_amount employees.salary%TYPE;
    e_invalid_employee EXCEPTION;
    PRAGMA EXCEPTION_INIT(e_invalid_employee, 100);
BEGIN
    -- check employee id before calling function
    SELECT employee_id INTO v_emp_id_check
        FROM employees WHERE employee_id = v_employee_id;
    -- call stored function to calculate tax amount
    -- pass employee_id as parameter
    v_tax_amount := sf_calculate_tax(v_employee_id);
    -- handle exceptions
    IF v_tax_amount = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Error calculating tax amount.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Tax to be paid: ' || v_tax_amount);
    END IF;
    EXCEPTION
    WHEN e_invalid_employee THEN
        DBMS_OUTPUT.PUT_LINE('Employee id ' || v_employee_id || '  is invalid.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Other problem occured');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```
