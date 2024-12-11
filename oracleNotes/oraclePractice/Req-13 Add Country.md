# Req-13: Add new country

Develop a stored procedure sp_add_country 
- to add a new country in Countries table. 
- The procedure accepts IN parameters 
    - country_id, 
    - country_name and 
    - region_id
- and status as OUT parameter OUT parameter status should be set as
    - 0 for successful insert
    - -1 if region_id is invalid 
    - -2 if country_id already exist
    - -3 for any other error
- Invoke the procedure sp_add_country to add Sydney(SN) with region_id as 6 (Australia).


## Stored Procedure

```sql 
CREATE OR REPLACE PROCEDURE sp_add_country(
    p_country_id IN countries.country_id%TYPE,
    p_country_name IN countries.country_name%TYPE,
    p_region_id IN countries.region_id%TYPE,
    p_status OUT NUMBER)
IS
    v_country_id_count NUMBER(2);
    v_region_id_count NUMBER(2);
BEGIN   
    -- check if country id exists
    SELECT COUNT(country_id) INTO v_country_id_count
        FROM countries WHERE country_id = p_country_id;
    IF v_country_id_count > 0 THEN
        p_status := -1;
    ELSE
        -- check valid region id4
        SELECT COUNT(region_id) INTO v_region_id_count 
            FROM regions WHERE region_id = p_region_id;
        IF v_region_id_count = 0 THEN
            p_status := -2;
        ELSE
            INSERT INTO countries
                (country_id, country_name, region_id)
                VALUES
                (p_country_id, p_country_name, p_region_id);
            COMMIT;
            p_status := 0;
        END IF;
    END IF;
    EXCEPTION
    WHEN OTHERS THEN
        p_status := -3;
END;
            
```

## Invoke Stored Procedure

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_country_id countries.country_id%TYPE := 'SN';
    v_country_name countries.country_name%TYPE := 'Sydney';
    v_region_id countries.region_id%TYPE := 8;
    v_result NUMBER(1,0);
BEGIN
    sp_add_country(v_country_id, v_country_name, v_region_id, v_result);
    IF v_result = 0 THEN
        DBMS_OUTPUT.PUT_LINE('Country successfully added');
    ELSIF v_result = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Invalid country id');
    ELSIF v_result = -2 THEN
        DBMS_OUTPUT.PUT_LINE('Invalid region id');
    ELSIF v_result = -3 THEN
        DBMS_OUTPUT.PUT_LINE('Other error');
    END IF;
END;
```