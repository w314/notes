# Oracle Packages

## Create Package Specification

```sql
CREATE OR REPLACE PACKAGE pkg_employee_info
IS
    FUNCTION get_manager_email(p_emp_id employees.employee_id%TYPE) RETURN VARCHAR2;

    PROCEDURE update_employee_phone(
        p_emp_id employees.employee_id%TYPE,
        p_new_phone employees.phone_number%TYPE,
        p_status OUT NUMBER);
END;
```

## Create Package Body

```sql
CREATE OR REPLACE PACKAGE BODY pkg_employee_info
IS
    -- define function
    -- define procedure
END;
```

## Use Package

```sql
DECLARE
    v_emp_id employees.employee_id%TYPE := 104;
    v_man_email employee.email%TYPE;
BEGIN
    v_man_email = pkg_employee_info.get_manager_email(v_emp_id);
    DBMS_OUTPUT.PUT_LINE('Manager Email: ' || v_man_email);
END;
```


## Built-In Packages

### DBMS

### Output ("Print") Results

```sql
-- if omitted it won't output anythin
SET SERVEROUTPUT ON;

-- print statemnt
DBMS_OUTPUT.PUT_LINE(v_variable_to_print |
| ' does not exist');
```


If encountering error: `PLS-00201: identifier 'DBMS.OUTPUT' must be declared`

Solve by running `GRANT EXECUTE ON DBMS_OUTPUT to PUBLIC;`

