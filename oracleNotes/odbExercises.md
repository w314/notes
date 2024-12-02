# Exercises

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

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.department_id%TYPE := 107;
    v_first_name employees.first_name%TYPE;
    v_phone_number employees.phone_number%TYPE;
BEGIN
    SELECT first_name, phone_number
        INTO v_first_name, v_phone_number
        FROM EMPLOYEES
        WHERE employee_id = v_employee_id;
    DBMS_OUTPUT.PUT_LINE('First Name: ' || v_first_name);
    DBMS_OUTPUT.PUT_LINE('Phone Number: ' || v_phone_number);
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

## Req-6 Add new job

HR Manager wants to add a new job Advertising Director (ADV_DIR).

Develop a PL/SQL program to add Advertising Director, ADV_DIR as a new job with minimum and maximum salary as 5000 and 10000 respectively. Add it to the database only if the same job ID does not exist, else display the message "ADV_DIR already exists".

```sql

```


