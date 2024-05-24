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
