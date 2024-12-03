# PL/SQL Constructs

## Operators

- `||` - concatenation
- `:=` - assignment
- logical
    - `AND`
    - `NOT`
    - `OR`

## Conditional Constructs

```sql
BEGIN
    -- one `=` only
    IF (v_id = 5) THEN
        statements;
    ELSIF <condition> THEN
        statements;
    ELSE
        statements;
    END IF;
END;
```

