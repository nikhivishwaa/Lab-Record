###### INSERT new Row into Table

```
INSERT INTO departments (department_id, department_name, manager_id, location_id)
VALUES (70,'Public_Relation',100,1700)
```

###### Default prototype
```
INSERT INTO departments
VALUES (132,'Public_Relation',100,1700)
```
###### Copying Data From one Table to Another Table
```
INSERT INTO department1
SELECT * FROM departments
```

###### Deleting Row From Table
```
DELETE FROM departments
    WHERE department_id = 270;
```

###### Enabling and Disabling Constraint
```
SELECT *
FROM SYS.USER_CONSTRAINTS
WHERE table_name = 'EMPLOYEE3'
```
```
ALTER TABLE employee3
DISABLE CONSTRAINT SYS_C004542
```
```
SELECT *
FROM employee3
```
```
DESC employee3
```
```
INSERT INTO employee3
VALUES (600,'susu',NULL,'gfgfgfg','hhhghgh','15JUN20','AD_VP',20000,0,130,80)
```
```
ALTER TABLE employee3
ENABLE CONSTRAINT SYS_C004542
```
```
DELETE employee3
WHERE last_name IS NULL
```
```
SELECT *
FROM employee3
```
```
ALTER TABLE employee3
ENABLE CONSTRAINT SYS_C004542
```
```
INSERT INTO employee3
VALUES (600,'susu',NULL,'gfgfgfg','hhhghgh','15JUN20','AD_VP',20000,0,130,80)
```
