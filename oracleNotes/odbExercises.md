# Exercises

Based on DB with tables stored under `./oraclePractice`.

## Req-1 Update the salary of employees

HR Manager wants to update the salary of employees

Based on the latest compensation review, the company has decided to give an annual hike of 10% to all its employees and an additional hike of 5% to its employees who have joined before '01-Jan-95'. 

HR manager wants to calculate the new salary of Alexander based on these rules, update the database and also display a report in the below format for employee with given ID.

Name : <First_Name> <Last_Name>
Date of Joining : <Hire_Date>
Current Salary : <Salary>
Incremented Salary : <Calculated Salary>

Try with ids: 103 & 107


```sql
SET SERVEROUTPUT ON;

DECLARE
    v_emp_id employees.employee_id%TYPE := 104;
    v_first_name employees.first_name%TYPE;
    v_last_name employees.last_name%TYPE;
    v_hire_date employees.hire_date%TYPE;
    v_current_salary employees.salary%TYPE;
    v_incremented_salary v_current_salary%TYPE;
BEGIN
    SELECT first_name, last_name, hire_date, salary
        INTO v_first_name, v_last_name, v_hire_date, v_current_salary 
        FROM employees
        WHERE employee_id = v_emp_id;
    IF v_hire_date < '01-JAN-95' THEN
        v_incremented_salary := v_current_salary * 1.15;
    ELSE
        v_incremented_salary := v_current_salary * 1.1;
    END IF;
    DBMS_OUTPUT.PUT_LINE('Name: ' || v_first_name || ' ' || v_last_name);
    DBMS_OUTPUT.PUT_LINE('Date of Joining: ' || v_hire_date);
    DBMS_OUTPUT.PUT_LINE('Current Salary: ' || v_current_salary);
    DBMS_OUTPUT.PUT_LINE('Increased Salary: ' || v_incremented_salary);
END;
```


## Req-2 View first name and phone number of employees

An employee wants to view the first name and phone number of other employees
- display a message if the employee is not present.
- try with id 107 (present) and 197 (not present) 

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.department_id%TYPE := 197;
    v_first_name employees.first_name%TYPE;
    v_phone_number employees.phone_number%TYPE;
BEGIN
    SELECT first_name, phone_number
        INTO v_first_name, v_phone_number
        FROM EMPLOYEES
        WHERE employee_id = v_employee_id;
    DBMS_OUTPUT.PUT_LINE('First Name: ' || v_first_name);
    DBMS_OUTPUT.PUT_LINE('Phone Number: ' || v_phone_number);
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Employee with ID: ' || v_employee_id || ' does not exists.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong!');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```

## Req-3 None
Same as before just show hire_date as well.

## Req-4 Eligible for tax?
An employee wants to check if he/she is eligible to pay tax. Employees having salary greater than 8000 are eligible to pay tax
Develop a PL/SQL program to check if Steven King, employee ID 100, is eligible to pay tax.

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 103;
    v_salary employees.salary%TYPE;
    v_eligible_salary CONSTANT NUMBER(6) := 8000;
BEGIN
    SELECT salary INTO v_salary
        FROM employees WHERE employee_id = v_employee_id;
    DBMS_OUTPUT.PUT_LINE('Eligible to pay tax if salary is at least: ' || v_eligible_salary);
    IF v_salary >= v_eligible_salary THEN
        DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary || ' ->  Eligible to pay tax.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary || ' -> Not eligible to pay tax.');
    END IF;
END;
```

## Req-5 Calculate Tax

Employees need to pay tax to the government based on the given salary slabs
Develop a PL/SQL program to calculate and display the tax amount of Steven King, employee ID 100.
Demosteps:
Tax is computed based on the below rules:
salary >= 15000 -> 15%
salary >= 8000 -> 10%
below 8000 0%

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 103;
    v_salary employees.salary%TYPE;
    v_tax_rate NUMBER(2);
    v_tax_amount NUMBER(8.2);
BEGIN
    SELECT salary INTO v_salary
        FROM employees WHERE employee_id = v_employee_id;
    IF v_salary >= 15000 THEN
        v_tax_rate := 15;
    ELSIF v_salary >= 8000 THEN
        v_tax_rate := 10;
    ELSE
        v_tax_rate := 0;
    END IF;
    v_tax_amount := v_salary * v_tax_rate / 100;
    DBMS_OUTPUT.PUT_LINE('Employee ID: ' || v_employee_id);
    DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);
    DBMS_OUTPUT.PUT_LINE('Tax Rate: ' || v_tax_rate);
    DBMS_OUTPUT.PUT_LINE('Tax Amount: ' || v_tax_amount);
END;
```

## Req-7 missing

## Req-8 Update comission
Develop a PL/SQL program to update the commission percentage(Commission_PCT) of Pat, employee ID 202, as 0.1, if he is a marketing rep (Job_ID :MK_REP). Also calculate and display the total salary of Pat.

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.department_id%TYPE := 202;
    v_commission_pct employees.commission_pct%TYPE := 0.1;
    v_job_id employees.job_id%TYPE;
    v_desired_job_id v_job_id%TYPE := 'MK_REP';
    v_salary employees.salary%type;
    v_total_salary v_salary%TYPE;
BEGIN
    SELECT job_id, salary INTO v_job_id, v_salary 
        FROM employees WHERE employee_id = v_employee_id;
    -- check if employee is a marketing rep 
    IF ( v_job_id = v_desired_job_id ) THEN
        UPDATE employees SET commission_pct = v_commission_pct
            WHERE employee_id = v_employee_id;
        v_total_salary := v_salary * (1 + v_commission_pct);
        DBMS_OUTPUT.PUT_LINE('Total Salary: ' || v_total_salary);
    END IF;
END;
```
## Req-9 missing

## Req-10  Nested Blocks - Add Employee
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

## Req-11 View employee dateils

HR manager wants to view all the details of an employee Joy Bosh (employee ID: 900), who has recently joined.

Develop a PL/SQL program to display all the details of an employee Joy Bosh.

USED employee with id 100 as 900 did not exist.

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

## Req-12 same as 11

## Req-13 Add new country

nfoSpark decided to expand their business in two more countries Singapore (SG) and Sri Lanka (LK) in Asia region.

Write a PL/SQL block to add these countries to DB. Check before adding country, whether they already exist. If exists, then don't add them to DB and display appropriate message.

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_country_id countries.country_id%TYPE := 'SG';
    v_country_name countries.country_name%TYPE := 'Singapore';
    v_region_name regions.region_name%TYPE := 'Asia';
    v_region_id regions.region_id%TYPE;
BEGIN
    SELECT region_id INTO v_region_id 
        FROM regions WHERE region_name = v_region_name;
    INSERT INTO countries
        ( country_id, country_name, region_id )
        VALUES ( v_country_id, v_country_name, v_region_id );
END;
```

## Reg-14 Number of Employees Per Job

HR manager needs a report that shows how many employees are working on a particular job.

Write a PL/SQL code to get report for 'Programmer' job.

Before generating report, given job should be checked whether it is valid or not. If not, display appropriate message.

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_job_id jobs.job_id%TYPE;
    v_job_title jobs.job_title%TYPE := 'Programmer';
    v_job_title_count NUMBER(2);
    v_employee_count NUMBER(2);
BEGIN
    SELECT COUNT(job_title) INTO v_job_title_count 
        FROM jobs WHERE job_title = v_job_title;
    IF v_job_title_count = 1 THEN
        SELECT job_id INTO v_job_id 
            FROM jobs WHERE job_title = v_job_title;
        SELECT COUNT(employee_id) INTO v_employee_count
            FROM employees WHERE job_id = v_job_id;
        DBMS_OUTPUT.PUT_LINE(v_employee_count || ' employees are working on the job ' || v_job_title);
    ELSE 
        DBMS_OUTPUT.PUT_LINE(v_job_title || ' is invalid job');
    END IF;
END;
```

## Req-15 Eligible for Promotion

Develop a PL/SQL program to check eligibility of David Austin, employee ID 105, for promotion. Employee should have completed at least 2 years with InfoSpark to be eligible for promotion.

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 105;
    v_hire_date employees.hire_date%TYPE;
    v_first_name employees.first_name%TYPE;
    v_months_between NUMBER(3);
BEGIN
    SELECT first_name, hire_date INTO v_first_name, v_hire_date 
        FROM employees WHERE employee_id = v_employee_id;
    DBMS_OUTPUT.PUT_LINE(v_first_name || ' was hired on: ' || v_hire_date);
    SELECT MONTHS_BETWEEN(SYSDATE, v_hire_date) INTO v_months_between
        FROM DUAL;
    IF ( v_months_between >= 24 ) THEN
        DBMS_OUTPUT.PUT_LINE('Eligible for promotion');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Not eligible for promotion');
    END IF;
END;
```

## Req-16 Update manager of department
HR Manager wants to update the manager details of a department.

Develop a PL/SQL program to make David Austin, employee ID 105, as the manager of IT department.

Business Rule: 105 should be a valid employee and should also belong to IT department.

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id departments.department_id%TYPE;
    v_department_name departments.department_name%TYPE := 'IT';
    v_employee_id employees.employee_id%TYPE := 105;
    v_employee_department_id employees.department_id%TYPE;
    v_employee_count NUMBER(2);
BEGIN   
    -- check if employee ID valid
    SELECT COUNT(employee_id) INTO v_employee_count
        FROM employees WHERE employee_id = v_employee_id;
    IF ( v_employee_count = 1 ) THEN
        -- check if employee belongs to IT department
        -- get id of department based on its name
        SELECT department_id INTO v_department_id 
            FROM departments WHERE department_name = v_department_name; 
        -- get department_id of employee
        SELECT department_id INTO v_employee_department_id 
            FROM employees WHERE employee_id = v_employee_id;
        -- check if employee belongs to the department    
        IF ( v_employee_department_id = v_department_id ) THEN
            -- update manager of department
            UPDATE departments SET manager_id = v_employee_id 
                WHERE department_id = v_department_id;
            DBMS_OUTPUT.PUT_LINE('Set manager_id of ' || v_department_name || ' department to ' ||  v_employee_id || '.');
        ELSE
            DBMS_OUTPUT.PUT_LINE('Employee does not belong to department ' || v_department_name);
        END IF;
    ELSE
        DBMS_OUTPUT.PUT_LINE('Invalid employee ID');
    END IF;
END;
```

## Req-17 View Job History of Employee

Develop a PL/SQL program to view the employee ID, start date, end date, job ID of employee with employee ID 103 and display appropriate message if the employee doesn't have job history.
- If more than one records are available in job_history table for the same employee then get the latest one.
- handle exceptions, if any, with appropriate message
- include WHEN OTHERS exception handler.
- try with id: 100 for one with job history



```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id job_history.employee_id%TYPE := 103;
    v_start_date job_history.start_date%TYPE;
    v_end_date job_history.end_date%TYPE;
    v_job_id job_history.job_id%TYPE;
BEGIN
    SELECT employee_id, start_date, end_date, job_id
        INTO v_employee_id, v_start_date, v_end_date, v_job_id
        FROM job_history WHERE employee_id = v_employee_id
        FETCH FIRST 1 ROWS ONLY;
    DBMS_OUTPUT.PUT_LINE('ID: ' || v_employee_id || ' worked job: ' || v_job_id ||
        ' from: ' || v_start_date || ' to: ' || v_end_date);
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Employee ID ' || v_employee_id || ' has no job history.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```

## Req-19 View Employee Manager's Details

DOES NOT WORK, DOES NOT RAISE USER DEFINED EXCEPTION 

- HR Manager wants to view manager's details of an employee
Develop a PL/SQL program to view the manager's details
    - first name
    - phone number 
    - of department 60. 
- Declare, raise and handle a user-defined exception if manager is not assigned to the department.

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id departments.department_id%TYPE := 77;
    v_manager_id departments.manager_id%TYPE;
    v_first_name employees.first_name%TYPE;
    v_phone_number employees.phone_number%TYPE;
    e_manager_not_assigned EXCEPTION;
BEGIN
    SELECT manager_id INTO v_manager_id 
        FROM departments WHERE department_id = v_department_id;
    IF ( v_manager_id IS NULL ) THEN
        RAISE e_manager_not_assigned;
    END IF;
    SELECT first_name, phone_number INTO v_first_name, v_phone_number
        FROM employees WHERE employee_id = v_manager_id;
    DBMS_OUTPUT.PUT_LINE('First Name: ' || v_first_name);
    DBMS_OUTPUT.PUT_LINE('Phone Number: ' || v_phone_number);
    EXCEPTION
    WHEN e_manager_not_assigned THEN
        DBMS_OUTPUT.PUT_LINE('Department ' || v_department_id || ' does not have a manager.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```

## Req-20 Add department

Develop a PL/SQL program to add a new department with
- DEPARTMENT_ID: 111
- DEPARTMENT_NAME: Sales
- MANAGER_ID: 222
- LOCATION_ID: 1500

In the program
- Declare, raise and handle a user-defined exception with an appropriate message if manager ID is not valid.
- Declare, raise and handle a user-defined exception with an appropriate message if location ID is not valid. 
- test location_id 150 for invalid location
- test manager_id 105 for valid manager

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id departments.department_id%TYPE := 111;
    v_department_name departments.department_name%TYPE := 'Sales';
    v_manager_id departments.manager_id%TYPE := 105;
    v_location_id departments.location_id%TYPE := 150;
    e_invalid_manager EXCEPTION;
    e_invalid_location EXCEPTION;
BEGIN
    DECLARE
        v_manager_count NUMBER(2);
    BEGIN
        SELECT COUNT(manager_id) INTO v_manager_count
            FROM employees WHERE employee_id = v_manager_id;
        IF v_manager_count = 0 THEN
            RAISE e_invalid_manager;
        END IF;
    END;
    DECLARE
        v_location_count NUMBER(2);
    BEGIN
        SELECT COUNT(location_id) INTO v_location_count
            FROM locations WHERE location_id = v_location_id;
        IF v_location_count = 0 THEN
            RAISE e_invalid_location;
        END IF;
    END;
    INSERT INTO departments
        (department_id, department_name, manager_id, location_id)
        VALUES
        (v_department_id, v_department_name, v_manager_id, v_location_id);
    DBMS_OUTPUT.PUT_LINE('New department created');
    EXCEPTION
    WHEN e_invalid_manager THEN
        DBMS_OUTPUT.PUT_LINE('Manager ID ' || v_manager_id || ' is invalid.');
    WHEN e_invalid_location THEN
        DBMS_OUTPUT.PUT_LINE('Location ID ' || v_location_id || ' is invalid.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```
