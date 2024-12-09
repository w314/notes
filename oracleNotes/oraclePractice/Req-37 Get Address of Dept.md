# Req-37: Get the address of a department based on department ID

Develop a stored function sf_get_location_address 
- that accept department ID and 
- should return the complete location address as VARCHAR2(1000) with comma separated (<street_address><,>< city><,>< state_province><-><postal_code><,><country_name>). 
- In case of exception, function returns -1.
- Invoke the function for department ID 30 and 31.

## Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_get_location_address(
    p_department_id departments.department_id%TYPE)
    RETURN VARCHAR2
IS
    v_location_id departments.location_id%TYPE;
    rec_location locations%ROWTYPE;
    v_country_name countries.country_name%TYPE;
BEGIN
    SELECT location_id INTO v_location_id 
        FROM departments WHERE department_id = p_department_id;
    SELECT * INTO rec_location
        FROM locations WHERE location_id = v_location_id;
    SELECT country_name INTO v_country_name
        FROM countries WHERE country_id = rec_location.country_id;
    RETURN rec_location.street_address || ', ' ||
        rec_location.city || ', ' ||
        rec_location.state_province || ', ' ||
        rec_location.postal_code || ', ' ||
        v_country_name;
    EXCEPTION
    WHEN OTHERS THEN
        RETURN '-1';
END;
```

## Invoke Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id departments.department_id%TYPE := 30;
    v_address VARCHAR2(1000);
BEGIN
    v_address := sf_get_location_address(v_department_id);
    IF v_address = '-1' THEN
        DBMS_OUTPUT.PUT_LINE('Error');
    ELSE 
        DBMS_OUTPUT.PUT_LINE(v_address);
    END IF;
END;
```