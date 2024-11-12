Execute the PL/SQL program to add Joy to the database, his details are:

EMPLOYEE_ID : 900

FIRST_NAME : Joy

LAST_NAME : Bosh

EMAIL : Joy_Bosh

HIRE_DATE: Today's date

JOB_ID: FI_MGR

```sql
DECLARE
  v_first_name VARCHAR2 (20) := 'Joy';
  v_last_name  VARCHAR2 (25) := 'Bosh';
  v_email      VARCHAR2 (25) := 'Joy_Bosh';
  --hire date is today's date,retrieved from database time
  v_hire_date   DATE          := SYSDATE;
  v_job_id      VARCHAR2 (10) := 'FI_MGR';
  v_employee_id NUMBER (6)    :=900;
BEGIN
  --employee Joy Bosh added to employees table
  INSERT
  INTO employees
    (
      EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,HIRE_DATE,JOB_ID
    )
    VALUES
    (
      v_employee_id,v_first_name,v_last_name,v_email,v_hire_date,v_job_id
    );
END;
 ```
