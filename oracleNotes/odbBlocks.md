# PL/SQL Blocks

```sql
-- instructs SQL Developer to echo output to the screen
SET SERVEROUTPUT ON;

-- declare variables
DECLARE
    -- customary to start variable names with v_
    -- name and type of variable are requred
    v_first_name VARCHAR2(20);
    -- use := for assignment
    v_employee_id PLS_INTEGER := 102;
-- business logic
BEGIN
    -- use INTO to store values retrived from database
    SELECT first_name INTO v_first_name
        FROM employees WHERE employee_id = v_employee_id;
    -- display text on screen
    DBMS_OUTPUT.PUT_LINE('Employee name: ' || v_first_name);
END;
```

## Anchored Delcaration

### Scalar Anchoring

#### anchor to table column data type

```sql
DECLARE
    v_first_name employees.first_name%TYPE;
```
- program will work even if data type is altered
- only datatype and size is referred
- NOT the contraints

#### anchor to other variable data type
```sql
DECLARE
    v_first_name VARHCAR2(20);
    v_last_name v_first_name%type;
```
- v_last_name will look up the type of the refered variabl at every compilation
- if data type changes only need to change it once
- constrains WILL get applied too


### Record Anchoring

- uses `%ROWTYPE`
- defines record structure based on a table or a predefined PL/SQL cursor


```sql
SET SERVEROUTPUT ON;

DECLARE
    rec_emp_details employees%ROWTYPE;
    v_employee_id employees.employee_id%TYPE := 100;
BEGIN
    SELECT * INTO rec_emp_details
        FROM employees WHERE employee_id = v_employee_id;
    DBMS_OUTPUT.PUT_LINE('Employee ID: ' || rec_emp_details.employee_id);
    DBMS_OUTPUT.PUT_LINE('First Name: ' || rec_emp_details.first_name);
END;
```
- name & datatypes of fields will be the same as in the table
- constrains are NOT applied
- when select either use `*` or list all column names
- retrieved values are stored in RECORD `rec_emp_detail`
- to refer to individual column use `rec_emp_detail.first_name`

## Nested Block

Blocks can be nested:
- in the execution part
- in the exception handling part

Variable Scope
- inner block variables are scoped to inner block
- when declared with same name as in outer block
    - inner variable gets preference
    - outer variable can be called using a `qualified name`

THIS BELOW IS NOT WORKING
```sql
/*Qualifying Identifier for outer block*/
<<outer_block>>
DECLARE
    v_tax_per NUMBER;
BEGIN
    v_tax_per := 7;
    /*Qualifying Identifier for inner block*/
    <<inner_block>>
    DECLARE
       v_tax_per NUMBER;
    BEGIN
       v_tax_per := 3;
       /*though variable declared in inner and outer block,
       variables can be differentiated using Qualifying Identifier*/
       DBMS_OUTPUT.PUT_LINE('in inner block v_tax_per: '||outer_block.v_tax_per);
       DBMS_OUTPUT.PUT_LINE('in inner block v_tax_per: '||inner_block.v_tax_per);
    END;
    /* we can not access the variable beyond the scope, even with the Qualifying Identifier*/
END;
```



Problem:
whenever a new employee is recruited to the company, HR manager should add the employee's details to the database. Certain validations need to be performed, before allocating employee to particular department and job.

Check if department name exists or not. If exists, get department ID from Departments table.

Check if job title exists or not. If exists, get job ID from Jobs table.

Execute the PL/SQL program to add Steve to the database, his details are

EMPLOYEE_ID : 902

FIRST_NAME : Steve

LAST_NAME : Belly

EMAIL : Steve_Belly

HIRE_DATE: Today's date

JOB_TITLE : Finance Manager

DEPARTMENT_NAME : Finance

```sql
 DECLARE
   v_employee_id       employees.employee_id%TYPE:=902;
   v_first_name        employees.first_name%TYPE := 'Steve';
   v_last_name         employees.last_name%TYPE := 'Belly';
   v_email             employees.email%TYPE := 'Steve_Belly';
   v_hire_date         employees.hire_date%TYPE := SYSDATE; --hire date is todays date,retrieved from database time
   v_department_name   departments.department_name%TYPE := 'Finance';
   v_job_title         jobs.job_title%TYPE := 'Finance Manager';
   v_department_id     departments.department_id%TYPE;
   v_job_id            jobs.job_id%TYPE;
BEGIN
       /* logic to validate department name and to get department ID   */
       DECLARE
          v_count_department   NUMBER (1);
       BEGIN
          SELECT COUNT (department_name)INTO v_count_department FROM departments WHERE department_name = v_department_name;
          /* check given department name available or not*/
          IF (v_count_department = 1) THEN
             SELECT department_id INTO v_department_id FROM departments WHERE department_name = v_department_name;
                 /* logic to validate job title and if valid get job ID   */
                 DECLARE
                    v_count_job   NUMBER (1);
                 BEGIN
                    SELECT COUNT (job_title) INTO v_count_job FROM jobs WHERE job_title = v_job_title;
                    /*to check given job Title  available or not*/
                    IF (v_count_job = 1) THEN
                       SELECT job_id INTO v_job_id FROM jobs WHERE job_title = v_job_title;
                       --IF Job ID valid then add employee to database
                       INSERT INTO employees (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,HIRE_DATE,JOB_ID,DEPARTMENT_ID)
                            VALUES (v_employee_id,v_first_name,v_last_name,v_email,v_hire_date,v_job_id,v_department_id);
                       COMMIT;
                    ELSE
                       DBMS_OUTPUT.put_line ('given job title '||v_job_title ||' does not exist');
                    END IF;
                 END;
          ELSE
             DBMS_OUTPUT.put_line ('given department || v_department_name '||' does not exist');
          END IF;
       END;
END;
```