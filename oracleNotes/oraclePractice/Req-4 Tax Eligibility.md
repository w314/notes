
## Req-4 Eligible for tax?

Develop a PL/SQL program to check if employee is eligible to pay tax.
- Develop a stored function sf_tax_eligibility to check if employee is eligible to pay tax.
- Employees having salary greater than 8000 are eligible to pay tax
- check for employee id 
    - 200 - not eligible
    - 99 - invalid id
    - 103 - eligible


### Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_tax_eligibility(
    p_employee_id employees.employee_id%TYPE)
    RETURN BOOLEAN
IS
    v_salary employees.salary%TYPE;
    v_tax_eligibility BOOLEAN;
    v_eligible_salary employees.salary%TYPE := 8000;
BEGIN
    SELECT salary INTO v_salary
        FROM employees WHERE employee_id = p_employee_id;
    IF v_salary > v_eligible_salary THEN
        v_tax_eligibility := TRUE;
    ELSE 
        v_tax_eligibility := FALSE;
    END IF;
    RETURN v_tax_eligibility;
    EXCEPTION
        WHEN OTHERS THEN
            RETURN NULL;
END;
```

### Invoking Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.department_id%TYPE := 103;
    v_emp_id_check v_employee_id%TYPE;
    v_tax_eligibility BOOLEAN;
BEGIN
    -- check valid employee id
    SELECT v_employee_id INTO v_emp_id_check 
        FROM employees WHERE employee_id = v_employee_id;
    v_tax_eligibility := sf_tax_eligibility(v_employee_id);
    IF(v_tax_eligibility) THEN
        DBMS_OUTPUT.PUT_LINE('Eligible to pay tax.');
    ELSIF(NOT v_tax_eligibility) THEN
        DBMS_OUTPUT.PUT_LINE('Not eligible to pay tax.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Error calculating tax eligiblity');
    END IF;
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Employee id ' || v_employee_id || ' is invalid');
END;
```