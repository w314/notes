# Req-28: add a new region in regions table.

- Develop a stored procedure sp_add_region which 

VERSION A
    - accepts region_id and region_name as IN parameter and 
    - set the OUT parameter status as 
        - 0 for successful insertion, 
        - -1 if region_id already exists and 
        -  -2 if region_name already exists. 
        - In case of exception, set the status as -3.
- Invoke the procedure with parameters as (6, Australia).

VERSION B
- Create Sequence for region id and use that to get id


## VERSION A

### Stored Procedure

```sql
CREATE OR REPLACE PROCEDURE sp_add_region(
    p_region_id IN regions.region_id%TYPE,
    p_region_name IN regions.region_name%TYPE,
    p_status OUT NUMBER)
IS
    v_id_count NUMBER(2);
    v_name_count NUMBER(2);
BEGIN
    SELECT COUNT(region_id) INTO v_id_count
        FROM regions WHERE region_id = p_region_id;
    IF v_id_count > 0 THEN
        p_status := -1;
    ELSE 
        -- check region name
        SELECT COUNT(region_name) INTO v_name_count
            FROM regions WHERE region_name = p_region_name;
        IF v_name_count > 0 THEN
            p_status := -2;
        ELSE 
            INSERT INTO regions 
                (region_id, region_name)
                VALUES
                (p_region_id, p_region_name);
            -- needs commit
            COMMIT;
            -- set status after successfull commit
            p_status := 0;
        END IF;
    END IF;
    EXCEPTION       
    WHEN OTHERS THEN
        p_status := -3;
END;
```

### Store New Region

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_region_id regions.region_id%TYPE := 6;
    v_region_name regions.region_name%TYPE := 'Asia';
    v_result NUMBER(1.0);
BEGIN
    -- call stored procedure
    sp_add_region(v_region_id, v_region_name, v_result);
    -- handle result
    DBMS_OUTPUT.PUT_LINE(v_result);
    IF v_result = 0 THEN
        DBMS_OUTPUT.PUT_LINE(v_region_name || ' is successfully added');
    ELSIF v_result = -1 THEN 
        DBMS_OUTPUT.PUT_LINE(v_region_id || ' region id already exists');
    ELSIF v_result = -2 THEN
        DBMS_OUTPUT.PUT_LINE(v_region_name || ' region name already exists');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Some Error Occured.');
    END IF;
END;
```


## VERSION B

### Create Sequence

```sql
CREATE SEQUENCE seq_region_id
    START WITH 8
    INCREMENT BY 1
    MAXVALUE 99;
```

### Create Procedure

```sql
CREATE OR REPLACE PROCEDURE sp_add_region_use_seq(
    p_region_name IN regions.region_name%TYPE,
    -- used to return region_id of inserted record
    p_region_id OUT regions.region_id%TYPE,
    -- used to return status of procedure excution
    p_status OUT NUMBER)
IS
    v_name_count NUMBER(2);
BEGIN
    -- check region name
    SELECT COUNT(region_name) INTO v_name_count
        FROM regions WHERE region_name = p_region_name;
    IF v_name_count > 0 THEN
        p_status := -2;
        -- finish procedure execution
        RETURN;
    END IF;
    -- get region id from sequence
    -- .NEXTVAL generates the next sequence
    INSERT INTO regions 
        (region_id, region_name)
        VALUES
        (seq_region_id.NEXTVAL, p_region_name);
    -- needs commit
    COMMIT;
    -- set status after successfull commit
    p_status := 0;
    -- set p_region_id to return id of created reagion
    p_region_id := seq_region_id.CURRVAL;
    EXCEPTION       
    WHEN OTHERS THEN
        p_status := -3;
END;
```

### Use Procedure

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_region_name regions.region_name%TYPE := 'As';
    v_region_id regions.region_id%TYPE;
    v_result NUMBER(1.0);
BEGIN
    -- call stored procedure
    sp_add_region_use_seq(v_region_name, v_region_id, v_result);
    -- handle result
    DBMS_OUTPUT.PUT_LINE(v_result);
    IF v_result = 0 THEN
        DBMS_OUTPUT.PUT_LINE(v_region_name || ' is successfully added with id ' || v_region_id);
    ELSIF v_result = -2 THEN
        DBMS_OUTPUT.PUT_LINE(v_region_name || ' region name already exists');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Some Error Occured.');
    END IF;
END;
```