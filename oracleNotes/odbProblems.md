
HR Manager wants to add a new job Advertising Director with id ADV_DIR.

Develop a PL/SQL program to add Advertising Director, ADV_DIR as a new job with minimum and maximum salary as 5000 and 10000 respectively. Add it to the database only if the same job ID does not exist, else display the message "ADV_DIR already exists".

```sql
declare
    v_job_id jobs.job_id%type := 'ADV_DIR';
    v_job_title jobs.job_title%type := 'Advertising Director';
    v_min_salary jobs.min_salary%type := 5000;
    v_max_salary jobs.max_salary%type := 10000;
    v_job_count number (2);
begin
    select count(job_id) into v_job_count from jobs where job_id = v_job_id;
    IF v_job_count > 0 THEN
        dbms_output.put_line(v_job_id || ' already exists.');
    ELSE 
        INSERT INTO jobs (job_id, job_title, min_salary, max_salary)
            values (v_job_id, v_job_title, v_min_salary, v_max_salary);
    end if;
end;
```