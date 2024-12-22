# Oracle Records

- `RECORD` makes it possible to store and access values as a group.
- use `RECORD` to group related items and pass them to a subprogram  as a single parameter


## Types of Records

- Table Based Record
    - table_name%ROWTYPE
- Cursor Based Record
    - cursor_name%ROWTYPE
- Programmer Defined Record
    - each field is defined separately with
        - name
        - data type
    - must be explicitely defined 
        - in PL/SQL `DECLARATION` block
        - or a `PACKAGE` specification
```sql
DECLARE
    -- define RECORD
    TYPE <type_name> IS RECORD
    (<field_name1> <datatype1>,
        <field_name2> <datatype2>,
        ...
        <field_nameN> <datatypeN>
    );
    -- declare record with type defined
    <record_name> <type_name>
BEGIN
    --- reference record field
    <record_name>.<field_name>
```sql




