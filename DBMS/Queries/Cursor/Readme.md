
###### SQL Command Line Usage
```
connect HR
```
```
SET SERVEROUTPUT ON
```

###### Cursor can access sql query result from memory area before obtaining complete result
```
declare cursor
open cursor
fetch cursor
close cursor
```

###### declare cursor
```
cursor c1 is SELECT * FROM employees
```
```
c1 => SELECT * FROM employees
```

###### Fetch Variable (attribute)
```
declare
cursor c1 is SELECT first_name, salary FROM employees;
vename employees.first_name%type;
vsal employees.salary%type;
begin
    open c1;
loop
    fetch c1 into vename, vsal;
    exit when c1%notfound;
dbms_output.put_line(vename||' '||vsal);
end loop;
close c1;
end;
/
```

###### Fetch row 
```
declare
cursor c1 is SELECT * FROM employees;
r employees%rowtype;
begin
    open c1;
loop
    fetch c1 into r;
    exit when c1%notfound;
dbms_output.put_line(r.first_name||' '||r.salary||' '||r.email);
end loop;
close c1;
end;
/
```

###### For Loop automatically handles the open and close cursor by itself

```
declare
cursor c1 is SELECT * FROM employees;
r employees%rowtype;
begin
    FOR r in c1
    loop
    dbms_output.put_line(r.first_name||' '||r.salary||' '||r.email);
    end loop;
end;
/
```

```
emp01
ename sal
A 5000
B 5400
C 5600
D 5500
E 4000
```

```
create table emp01(
    ename varchar2(4),
    sal number(6,2));
```

```
 INSERT INTO emply2 (ename, sal) VALUES ('&ename', &sal);
```

```
insert into emply2 values('&ename',&sal);
```


```
declare
cursor c1 is SELECT * FROM emp01;
begin
    FOR r in c1
    loop
    UPDATE emp01 SET sal = sal + 1000 WHERE ename = r.ename;
    end loop;
end;
/
```

```
declare
cursor c1 is SELECT * FROM emp01 for update of sal nowait;
begin
    FOR r in c1
    loop
    UPDATE emp01 SET sal = sal + 1000 WHERE current of c1;
    end loop;
end;
/
```

##### Parameterized Cursor

```
DECLARE
e employees%rowtype;
CURSOR e_sal(low_salary NUMBER, high_salary NUMBER)
IS 
    SELECT * 
    FROM employees
    WHERE salary BETWEEN low_salary AND high_salary;

BEGIN
    dbms_output.put_line('Low Salary employee: ');
    OPEN e_sal(2000,7000);
    LOOP
        FETCH e_sal INTO e;
        EXIT WHEN e_sal%notfound;
        dbms_output.put_line(e.first_name||': '||e.salary);
    END LOOP;
    CLOSE e_sal;


    OPEN e_sal(8000,2200);
    LOOP
        FETCH e_sal INTO e;
        EXIT WHEN e_sal%notfound;
        dbms_output.put_line(e.first_name||': '||e.salary);
    END LOOP;
    CLOSE e_sal;
END;
    /
```

##### Default Parameterized Cursor

```
DECLARE
e employees%rowtype;
CURSOR e_sal(low_salary NUMBER:=2000, high_salary NUMBER:=7000)
IS 
    SELECT * 
    FROM employees
    WHERE salary BETWEEN low_salary AND high_salary;

BEGIN
    -- Low Salary Employees
    dbms_output.put_line('Low Salary employee: ');
    OPEN e_sal;
    LOOP
        FETCH e_sal INTO e;
        EXIT WHEN e_sal%notfound;
        dbms_output.put_line(e.first_name||': '||e.salary);
    END LOOP;
    CLOSE e_sal;
END;
    /
```

```
DECLARE
e employees%rowtype;
CURSOR e_sal(low_salary NUMBER:=2000, high_salary NUMBER:=7000)
IS 
    SELECT * 
    FROM employees
    WHERE salary BETWEEN low_salary AND high_salary;

BEGIN
    -- Low Salary Employees

    OPEN e_sal(10000,20000);
    LOOP
        FETCH e_sal INTO e;
        EXIT WHEN e_sal%notfound;
        dbms_output.put_line(e.first_name||': '||e.salary);
    END LOOP;
    CLOSE e_sal;
END;
    /
```

##### Nested Cursor

```
DECLARE
e employees%rowtype;
d departments%rowtype;
dept_no employees.department_id%type;
CURSOR emp IS 
    SELECT * 
    FROM employees
    WHERE department_id = dept_no;

CURSOR dept IS 
    SELECT * 
    FROM departments;

BEGIN
    OPEN dept;
    LOOP
        FETCH dept INTO d;
        EXIT WHEN dept%notfound;
        dept_no:= d.department_id;

        dbms_output.put_line('---------------------------------------------------------------- ');
        dbms_output.put_line('Department '||d.department_name||' Employees :');
        dbms_output.put_line('---------------------------------------------------------------- ');
        
        OPEN emp;
        LOOP
            FETCH emp INTO e;
            EXIT WHEN emp%notfound;
            dbms_output.put_line('Employee: '||e.first_name||chr(9)||'Salary: '||e.salary);
        END LOOP;
        CLOSE emp;
    END LOOP;
    CLOSE dept;
END;
/
```


#### Exception Handling

###### ZERO_DIVIDE Exception
```
DECLARE
dividend NUMBER:= 10;
divisor NUMBER:= 0;
result NUMBER;

BEGIN
    BEGIN
        result:= dividend / divisor;
            dbms_output.put_line('Result: '||result);
        EXCEPTION
            WHEN ZERO_DIVIDE THEN
            dbms_output.put_line('Error: Zero Divison Error');
    END;
END;
/
```

###### NO_DATA_FOUND Exception
```
DECLARE
emp_name VARCHAR2(100);
emp_id NUMBER:= 255;

BEGIN
    BEGIN
        SELECT first_name INTO emp_name FROM employees WHERE employee_id = emp_id;
        dbms_output.put_line('Employee Name: '|| emp_name);
        EXCEPTION
            WHEN NO_DATA_FOUND THEN
            dbms_output.put_line('Error: no matching record found');
    END;
END;
/
```