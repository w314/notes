# PS/SQL Stored Procedure

> DO NOT COMMIT IN PROCEDURES
- let the calling code decide when is it logical to commit
- make rolling back possible for the colling code

## Define Procedure

 Create stored procedure sp_add_region
 - accepts region_id and region_name as IN parameter
 - set the OUT parameter status as 0 for successful insertion
 - -1 if region_id already exists
 - -2 if region_name already exists
 - in case of exception, set the status as -3.

```sql
-- naming convention to start name with sp_
CREATE OR REPLACE PROCEDURE sp_add_region(
    -- parameter with IN mode are used to 
    -- store values passed to the procedure
    -- these values are constants
    p_region_id IN regions.region_id%TYPE,
    p_region_name IN regions.region_name%TYPE,
    -- parameters with OUT mode are used to
    -- pass values from the procedure
    -- to the calling environment
    p_status OUT NUMBER)
IS
    v_count_of_id PLS_INTEGER;
    v_count_of_name PLS_INTEGER;
BEGIN
    -- check if region id already exist
    SELECT COUNT(region_id) INTO v_count_of_id
        FROM regions
        WHERE region_id = p_region_id;
    -- if region id does not exists
    IF v_count_of_id = 0 THEN
        -- check if name already exists
        SELECT COUNT(region_name) INTO v_count_of_name
        FROM regions
        WHERE region_name = p_region_name;
        -- if region name does not exist
        IF v_count_of_name = 0 THEN
            -- insert region into database
            INSERT INTO regions (region_id, region_name)
                VALUES (p_region_id, p_region_name);
            -- set status to 0 to show success
            p_status := 0;
        ELSE 
            -- region name already exists set status to -2
            p_status := -2;
            -- terminate procedure if region name already exists
            RETURN;
        END IF;
    ELSE
        -- region id already exists set status to -1
        p_status := -1;
        -- terminate procedure if id already exists
        RETURN;
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
    -- store value of OUT parameter
    v_status NUMBER(1, 0);
BEGIN
    -- invoke stored procedure
    -- pass variable for OUT parameter too
    sp_add_region(6, 'Asia', v_status);
    -- perform logic based on value of OUT parameter
    IF v_status = 0 THEN
        DBMS_OUTPUT.PUT_LINE('Reagion added successfully');
    ELSIF v_status = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Region ID already exists');
    ELSIF v_status = -2 THEN
        DBMS_OUTPUT.PUT_LINE('Region name already exists');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Other problem occured');
    END IF;
END;
```

## Passing Parameters to Stored Procedure

Techniques for passing parameters
```sql
-- POSITONAL NOTATION
sp_add_region(6, 'Asia', v_statu);

-- NAMED NOTATION
-- no need to keep order of parameters
sp_add_region(
    p_region_name=>'Asia', 
    p_status=>v_status,
    p_region_id=>6
);

-- MIXED NOTATION
-- first parameters specified useing postional notation
-- the rest by named notation
-- the reverse is not allowed
sp_add_region(
    6,
    p_status=>v_status,
    p_region_name=>'Asia'
);
```
