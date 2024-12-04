
# Req-18 Custom Exception - Eligible for Home Loan

Employee with the employee ID 105 wants to know whether he/she is eligible for home loan.
-  An employee is eligible for home loan only if his/her salary is greater than or equal to 8000. 
- If not eligible, raise an exception and handle with appropriate message.
- check with id 110 for eligible

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 105;
    v_salary employees.salary%TYPE;
    e_home_loan_eligibility EXCEPTION;
BEGIN
    SELECT salary INTO v_salary
        FROM employees WHERE employee_id = v_employee_id;
    IF ( v_salary < 8000 ) THEN
        RAISE e_home_loan_eligibility;
    END IF;
    DBMS_OUTPUT.PUT_LINE('Eligible for Home Loan');
    EXCEPTION
    WHEN e_not_eligible THEN
        DBMS_OUTPUT.PUT_LINE('Not eligible for Home Loan');
END;
```
