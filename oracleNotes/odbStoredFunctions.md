# PL/SQL Stored Functions

Stored Function to calculate tax amount
```sql
-- FUNCTION HEADER
-- naming convention: prefix function name with 'sf_'
CREATE OR REPLACE FUNCTION sf_tax_calc(
    -- parameters will store variables passed to the function
    p_employee_id employees.employee_id%TYPE)
RETURN NUMBER
-- DECLARATIVE SECTION
IS
    v_salary employees.salary%type;
    v_tax_rate number(2);
    v_tax_amount number(8,2);
-- EXECUTABLE SECTION
BEGIN
    -- get employee salary
    SELECT salary INTO v_salary 
        FROM employees
        WHERE employee_id = p_employee_id;
    -- determine tax rate based on salary
    IF v_salary >= 15000 THEN
        v_tax_rate := 15;
    ELSIF v_salary >= 8000 THEN
        v_tax_rate := 10;
    ELSE
        v_tax_rate := 0;
    END IF;
    -- calculate tax to be paid
    v_tax_amount := v_salary * (1 + v_tax_rate / 100);
    -- return tax to be paid
    RETURN v_tax_amount;
    exception
    when NO_DATA_FOUND then
        dbms_output.put_line('No employee wiht id: ' || p_employee_id);
end;
```
