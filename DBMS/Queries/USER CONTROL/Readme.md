###### CREATE NEW USER (Execute in SYS USER Terminal)

```
CREATE USER sistec
IDENTIFIED BY sistec
```

##### VERIFY PRIVILAGES
```
CREATE TABLE sumo (
    name VARCHAR2(20),
    roll NUMBER(10))
```

##### Execute in SYS USER Terminal

```
GRANT create session, create table, 
      create sequence, create view
TO sistec
```

###### Allocate Space to user from System space
```
ALTER USER sistec quota 200M on system
```

###### Create Role from SYS Terminal
```
CREATE ROLE manager
```

###### Grant privileges to role
```
GRANT create table, create view
TO manager
```

###### Grant Role To User
```
GRANT manager
TO sistec1
```

###### Allocate Space to user from System space
```
ALTER USER sistec1 quota 200M on system
```

### Object Level Privileges

###### Execute in HR's Terminal 
```
GRANT select
ON employees
TO sistec1, sistec
```

###### Execute in sistec OR sistec1's Terminal 
```
SELECT * 
FROM HR.employees
```

###### Grant only selected column access (Execute in HR's Terminal)
```
GRANT update (department_name, location_id)
ON departments
TO sistec1, sistec
```

###### Grant sharable privileges wich can be pass on to other user (Execute in HR's Terminal)
```
GRANT select, insert, update
ON departments
TO sistec1
WITH GRANT OPTIONS
```

###### Revoke object level privileges

```
REVOKE select
ON departments
FROM sistec1
```