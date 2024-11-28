# Oracle Data Types

## `VARCHAR` vs `VARCHAR2`

`VARCHAR2` does not distinguish between `NULL` and empty values. `VARCHAR` does.


## PL/SQL Data Types

### `PLS_INTEGER`

- specific to `PL/SQL`
- represents `signed 32 bits integers`
- range from -2,147,483,648 to 2,147,483,647
- uses **hardware arithmetic** (vs software arithmetic that `NUMBER` uses)
- which makes it **faster**
- requires **less storage** than `NUMBER`

## CONSTANT
Use `CONSTANT` to declare a constant.
