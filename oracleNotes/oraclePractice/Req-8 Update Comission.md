
## Req-8 Update comission

Develop a stored procedure sp_update_comm_pct 
- to update the commission percentage (Commission_PCT) 
    - as 0.1 of employees working as marketing rep (Job_ID :MK_REP). 
- The procedure accepts 
    - IN employee ID as 
    - status as OUT parameter.
- OUT parameter status should be set as
    - 0 for successful update
    - -1 if employee_id is invalid 
    - -2 if employee is not a marketing rep
    - -3 for any other error
- Invoke the procedure with employee ID as 202, 100 and 115.

## Store Procedure

```sql
CREATE OR REPLACE PROCEDURE sp_update_commission(
    p_employee_id employees.employee_id%TYPE,
    p_status OUT NUMBER)
IS
    c_new_commission CONSTANT employees.commission_pct%TYPE := 0.1;
    c_job_id_to_update CONSTANT employees.job_id%TYPE := 'MK_REP';
    v_emp_id_count NUMBER(2);
    v_employee_job_id employees.job_id%TYPE;
BEGIN
    SELECT job_id INTO v_employee_job_id
        FROM employees WHERE employee_id = p_employee_id;
    -- handle employee not working in the department
    IF v_employee_job_id != c_job_id_to_update THEN
        p_status := -2;
    ELSE
        -- update commission
        UPDATE employees
            SET commission_pct = c_new_commission
            WHERE employee_id = p_employee_id;
        COMMIT;
        -- set status to success
        p_status := 0;
    END IF;
    EXCEPTION 
    -- handle invalid employee id
    WHEN NO_DATA_FOUND THEN
        p_status := -1;
    WHEN OTHERS THEN
        p_status := -3;
END;
```


## Invoke Stored Procedure

Also calculate and display the total salary.
- use 202 for valid employee id
- use 124 employee not in proper department

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.department_id%TYPE := 124;
    v_salary employees.salary%type;
    v_commission_pct employees.commission_pct%TYPE;
    v_total_salary v_salary%TYPE;
    v_result NUMBER(1);
BEGIN
    sp_update_commission(v_employee_id, v_result);
    IF v_result = 0 THEN
        SELECT salary, commission_pct INTO v_salary, v_commission_pct
            FROM employees WHERE employee_id = v_employee_id;
        v_total_salary := v_salary * (1 + v_commission_pct);
        DBMS_OUTPUT.PUT_LINE('New total Salary: ' || v_total_salary);
    ELSIF v_result = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Invalid employee id');
    ELSIF v_result = -2 THEN
        DBMS_OUTPUT.PUT_LINE('Employee is not eligible for commission update');
    ELSIF v_result = -3 THEN
        DBMS_OUTPUT.PUT_LINE('Error while updating commission');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Unexpected error');
    END IF;
END;
```
