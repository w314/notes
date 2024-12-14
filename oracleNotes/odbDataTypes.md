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
```sql
c_days_per_year CONSTANT NUMBER(3.0):= 365;
```

## DATE

- [Date Function - OracleTutorial](https://www.oracletutorial.com/oracle-date-functions/)
- [MONTHS_BETWEEN example](https://www.oracletutorial.com/oracle-date-functions/oracle-months_between/)


### Extract
[Extract -  Databasestar](https://www.databasestar.com/oracle-extract/)

To extract local hour:
```sql
EXTRACT(HOUR FROM SYSTIMESTAMP) + EXTRACT(TIMEZONE_HOUR FROM SYSTIMESTAMP)
```
- `EXTRACT(HOUR ...)` by itself returns UTC time

### Interval between dates

```sql
-- returns current system date & time
-- of the operation system oracle runs
SYSDATE
-- returns the number of months between two dates.
MONTHS_BETWEEN

-- '-' returns the number of days between dates
v_days_hired := SYSDATE - v_hire_date;
```

### Get Month From Date

```sql
SELECT TO_CHAR(SYSDATE, 'Month) FROM DUAL;
-- OR
SELECT TO_CHAR(TO_DATE('02-11-2024', 'DD-MM-YYYY'), 'Month') FROM DUAL;
```

### Get number or name of day from date
[Source - Database.guide](https://database.guide/2-ways-to-get-the-day-from-a-date-in-oracle/)

```sql
SELECT TO_CHAR(DATE '2024-1206', 'DAY') FROM DUAL;
-- friday
```
