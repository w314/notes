# Req-7 Update Phone Number

Develop a stored procedure sp_update_contact
-  which accepts employee ID and new phone number as IN parameters, 
- status as OUT parameter, 
    - status is set as 0 if update is successful,
    - -1 if employee_id is invalid and 
    - -2 in case of any other exception.

### Stored Procedure

```sql
CREATE OR REPLACE PROCEDURE sp_update_phone(
    p_employee_id IN employees.employee_id%TYPE,
    p_phone_number IN employees.phone_number%TYPE,
    p_status OUT NUMBER)
IS
    v_id_count NUMBER(2);
BEGIN
    SELECT COUNT(employee_id) INTO v_id_count
        FROM employees WHERE employee_id = p_employee_id;
    IF v_id_count = 0 THEN
        p_status := -1;
    ELSE 
        UPDATE employees SET phone_number = p_phone_number
            WHERE employee_id = p_employee_id;
        COMMIT;
        p_status := 0;
    END IF;
    EXCEPTION
    WHEN OTHERS THEN
        p_status := -2;
END;
```


### Use Stored Procedure

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 138;
    v_phone_number employees.phone_number%TYPE := '650.122.2022';
    v_result NUMBER(1.0);
BEGIN
    sp_update_phone(v_employee_id, v_phone_number, v_result);
    IF v_result = 0 THEN
        DBMS_OUTPUT.PUT_LINE('Phone number updated successfully');
    ELSIF v_result = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Invalid employee id');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Other error occured');
    END IF;
END;
```