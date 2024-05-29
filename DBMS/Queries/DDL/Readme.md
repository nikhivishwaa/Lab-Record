###### CREATE Table

```
CREATE TABLE dept
        (deptno NUMBER(2),
          dname VARCHAR2(14),
          loc VARCHAR2(13),
          create_table DATE DEFAULT SYSDATE);
```
###### Column Level Constraint
```
CREATE TABLE employee1(
        employee_id NUMBER(6)
          CONSTRAINT employee1_emp_id_pk PRIMARY KEY,
        first_name VARCHAR2(20),
        last_name VARCHAR2(25),
        email VARCHAR2(25) NOT NULL,
        phone_number VARCHAR2(20) NOT NULL,
        hire_date DATE DEFAULT SYSDATE,
        job_id VARCHAR2(10) NOT NULL,
        salary NUMBER(8),
        commission_pct NUMBER(2),
        manager_id NUMBER(6),
        department_id NUMBER(4)
)
```

###### Table Level Constraint
```
CREATE TABLE employee2(
        employee_id NUMBER(6),
        first_name VARCHAR2(20) NOT NULL,
        last_name VARCHAR2(25) NOT NULL,
        email VARCHAR2(25) NOT NULL,
        phone_number VARCHAR2(20) NOT NULL,
        hire_date DATE DEFAULT SYSDATE,
        job_id VARCHAR2(10) NOT NULL,
        salary NUMBER(8),
        commission_pct NUMBER(2),
        manager_id NUMBER(6),
        department_id NUMBER(4),
        CONSTRAINT employee2_emp_id_pk
           PRIMARY KEY (EMPLOYEE_ID)
)
```

###### Creating Primary Key From More Than 1 Column
```
CREATE TABLE employee3(
        employee_id NUMBER(6),
        first_name VARCHAR2(20),
        last_name VARCHAR2(25) NOT NULL,
        email VARCHAR2(25) NOT NULL,
        phone_number VARCHAR2(20) NOT NULL,
        hire_date DATE DEFAULT SYSDATE,
        job_id VARCHAR2(10) NOT NULL,
        salary NUMBER(8),
        commission_pct NUMBER(2),
        manager_id NUMBER(6),
        department_id NUMBER(4),
        CONSTRAINT employee3_emp_id_phno_pk
           PRIMARY KEY (EMPLOYEE_ID, PHONE_NUMBER)
)
```

###### Creating Department1 Table and Copying Data From Departments
```
CREATE TABLE department1(
        department_id NUMBER(4),
        department_name VARCHAR2(30) NOT NULL,
        manager_id NUMBER(6),
        location_id NUMBER(4),
        CONSTRAINT department1_dept_id_pk
           PRIMARY KEY (DEPARTMENT_ID)
)
```
###### copying departments data into department1
```
INSERT INTO department1
SELECT * FROM departments
```

###### Creating Table with Foreign key
```
CREATE TABLE employee4(
        employee_id NUMBER(6),
        first_name VARCHAR2(20),
        last_name VARCHAR2(25) NOT NULL,
        email VARCHAR2(25) NOT NULL,
        phone_number VARCHAR2(20) NOT NULL,
        hire_date DATE DEFAULT SYSDATE,
        job_id VARCHAR2(10) NOT NULL,
        salary NUMBER(8),
        commission_pct NUMBER(2),
        manager_id NUMBER(6),
        department_id NUMBER(4),
        CONSTRAINT employee4_emp_id_phno_pk
           PRIMARY KEY (EMPLOYEE_ID, PHONE_NUMBER),
        CONSTRAINT45 employee4_dept_id_fk
           FORIEGN KEY (DEPARTMENT_ID)
              REFERENCES department1(department_id),
        CONSTRAINT employee4_email_uk
           UNIQUE(EMAIL)
)
```


###### Create Table from SubQuery
```
CREATE TABLE dept80
  AS
     SELECT employee_id, last_name, salary*12 Annual_Salary, hire_date
     FROM employees
     WHERE department_id = 80
```

##### ALTER TABLE

###### alter table to add new column
```
ALTER TABLE dept80
ADD (job_id VARCHAR2(9))
```

###### alter table to modify a column
```
ALTER TABLE dept80
MODIFY (last_name VARCHAR2(30))
```

###### alter table to dropping a column
```
ALTER TABLE dept80
DROP (job_id)
```

###### alter table to hide a column by marking unused
```
ALTER TABLE dept80
SET UNUSED (employee_id)
```

###### alter table dropping unused columns
```
ALTER TABLE dept80
DROP UNUSED COLUMNS
```

###### Dropping the Table (TABAHI)
```
DROP TABLE dept80
```

##### Enabling constraint in table - 

###### reating Primary Key
```
ALTER TABLE dept80
MODIFY employee_id PRIMARY KEY

```
###### OR
```
ALTER TABLE dept81
ADD CONSTRAINT emp_mgr_Pk
    PRIMARY KEY (employee_id)
```
