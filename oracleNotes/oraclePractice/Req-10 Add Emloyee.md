
## Req-10  Nested Blocks - Add Employee

Develop a stored procedure sp_add_employee
- which accepts 
    - first_name, 
    - last_name, email, 
    - hire_date, 
    - job_id, 
    - department_name as IN parameters and 
    - p_status as OUT parameter.
- OUT parameter p_status should be set as
    - 0 for insertion is successful
    - -1, if email is invalid (email ID considered as invalid if it is already present in the table )
    - -2, if hire_date is less than today’s date
    - -3, if job_id does not exist
    - -4, if department_name is invalid
    - -5, in case of any other exception
- Hint:
    - Employee ID should be auto generated using the sequence seq_employee_id created in previous exercise.
    - Get department_id using stored function sf_get_dept_id.
    - Get the manager_id from the department table based on department_id.
- Also invoke the procedure to add Adam to the database, his details are:
    - FIRST_NAME : Adam
    - LAST_NAME : Hilton
    - EMAIL : Adam_Hilton
    - HIRE_DATE: Today's date
    - JOB_ID: FI_ACCOUNT
    - DEPARTMENT_NAME: Finance


## Stored Procedure

```sql
CREATE OR REPLACE PROCEDURE sp_add_employee(
    p_first_name IN employees.first_name%TYPE,
    p_last_name IN employees.last_name%TYPE,
    p_email IN employees.email%TYPE,
    p_hire_date IN employees.hire_date%TYPE,
    p_job_id IN employees.job_id%TYPE,
    p_department_name IN departments.department_name%TYPE,
    p_status OUT NUMBER)
IS
    v_department_id departments.department_id%TYPE;
    v_manager_id employees.manager_id%TYPE;
    v_email_count NUMBER(2);
    v_job_id_count NUMBER(2);
BEGIN
    -- check valid email
    SELECT COUNT(email) INTO v_email_count 
        FROM employees WHERE email = p_email;
    IF v_email_count > 0 THEN
        p_status := -1;
        RETURN;
    END IF;
    
    IF p_hire_date < SYSDATE THEN
        p_status := -2;
        RETURN;
    END IF;
    
    SELECT COUNT(job_id) INTO v_job_id_count
        FROM jobs WHERE job_id = p_job_id;
    IF v_job_id_count = 0 THEN
        p_status := -3;
        RETURN;
    END IF;
    
    v_department_id := sf_get_dept_id(p_department_name);
    IF v_department_id = -1 THEN
        p_status := -4;
        RETURN;
    END IF;
    
    SELECT manager_id INTO v_manager_id
        FROM departments WHERE department_id = v_department_id;
    
    INSERT INTO employees
        (employee_id, first_name, last_name, email, 
         hire_date, job_id, manager_id, department_id)
        VALUES
        (seq_employee_id.NEXTVAL, p_first_name, p_last_name, p_email, 
         p_hire_date, p_job_id, v_manager_id, v_department_id);
    COMMIT;
    p_status := 0;
    EXCEPTION
    WHEN OTHERS THEN
        p_status := -5;
END;            
```

## Invoke Stored Procedure

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_first_name employees.first_name%TYPE := 'Adam';
    v_last_name employees.last_name%TYPE := 'Hilton';
    v_email employees.email%TYPE := 'Adam_Hilton1';
    v_department_name departments.department_name%TYPE := 'Finance';
    v_job_id jobs.job_id%TYPE := 'FI_ACCOUNT';
    v_hire_date employees.hire_date%TYPE := SYSDATE;
    v_result NUMBER(1,0);
BEGIN
    sp_add_employee(v_first_name, v_last_name, v_email, 
        v_hire_date, v_job_id, v_department_name, v_result);
    IF v_result = 0 THEN
        DBMS_OUTPUT.PUT_LINE('Employee successfully added');
    ELSIF v_result = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Invalid email');
    ELSIF v_result = -2 THEN
        DBMS_OUTPUT.PUT_LINE('Hire date is before today');
    ELSIF v_result = -3 THEN
        DBMS_OUTPUT.PUT_LINE('Invalid job id');
    ELSIF v_result = -4 THEN
        DBMS_OUTPUT.PUT_LINE('Invalid department name');
    ELSIF v_result = -5 THEN
        DBMS_OUTPUT.PUT_LINE('Other error');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Unexpected result: ' || v_result);
    END IF;
END;
```


## Old Version
whenever a new employee is recruited to the company, HR manager should add the employee's details to the database. Certain validations need to be performed, before allocating employee to particular department and job.

- Check if department name exists or not. If exists, get department ID from Departments table.
- Check if job title exists or not. If exists, get job ID from Jobs table.
- Execute the PL/SQL program to add Steve to the database, his details are
    - EMPLOYEE_ID : 902
    - FIRST_NAME : Steve
    - LAST_NAME : Belly
    - EMAIL : Steve_Belly
    - HIRE_DATE: Today's date
    - JOB_TITLE : Finance Manager
    - DEPARTMENT_NAME : Finance

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 902;
    v_first_name employees.first_name%TYPE := 'Steve';
    v_last_name employees.last_name%TYPE := 'Belly';
    v_email employees.email%TYPE := 'Steve_Belly';
    v_department_name departments.department_name%TYPE := 'Finance';
    v_job_title jobs.job_title%TYPE := 'Finance Manager';
    v_hire_date employees.hire_date%TYPE := SYSDATE;
    v_department_id employees.department_id%TYPE;
    v_job_id employees.job_id%TYPE;
    
BEGIN
    DECLARE       
        v_department_name_count NUMBER(2);
    BEGIN   
        SELECT COUNT(department_name) INTO v_department_name_count
            FROM departments WHERE department_name = v_department_name;
        IF ( v_department_name_count = 1 ) THEN
            SELECT department_id INTO v_department_id
                FROM departments WHERE department_name = v_department_name;
            DECLARE
               v_job_title_count NUMBER(2);
            BEGIN   
                SELECT COUNT(job_title) INTO v_job_title_count
                    FROM jobs WHERE job_title = v_job_title;
                IF ( v_job_title_count = 1 ) THEN
                   SELECT job_id INTO v_job_id
                       FROM jobs WHERE job_title = v_job_title; 
                   INSERT INTO employees
                       (employee_id, first_name, last_name, email, hire_date, job_id, department_id)
                       VALUES
                       (v_employee_id, v_first_name, v_last_name, v_email, v_hire_date, v_job_id, v_department_id);
                   DBMS_OUTPUT.PUT_LINE('Employee added to database');
                ELSE
                   DBMS_OUTPUT.PUT_LINE('Job title ' || v_job_title || ' does not exists.');
                END IF;
            END;
        ELSE
            DBMS_OUTPUT.PUT_LINE('Department name ' || v_department_name || ' does not exists.');
        END IF;
    END;
END;
```