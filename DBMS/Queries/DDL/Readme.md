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
CREATE TABLE copy_emp(
        employee_id NUMBER(6)
          CONSTRAINT cop_emp_emp_id_pk PRIMARY KEY,
        first_name VARCHAR2(20) NOT NULL,
        last_name VARCHAR2(20) NOT NULL
)
```
