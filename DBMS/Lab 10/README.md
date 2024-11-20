```
CREATE TABLE U_Department (
    DepartmentCode NUMBER(10) PRIMARY KEY,
    DepartmentName VARCHAR2(50) UNIQUE NOT NULL,
    OfficeNumber VARCHAR2(10) NOT NULL,
    OfficePhone CHAR(10) NOT NULL,
    College VARCHAR(50) NOT NULL
);

```

```
CREATE TABLE u_student (
    StudentID NUMBER(12) PRIMARY KEY,
    SSN CHAR(9) UNIQUE NOT NULL,
    FirstName VARCHAR2(50) NOT NULL,
    LastName VARCHAR2(50),
    CurrentAddress VARCHAR2(100) NOT NULL,
    CurrentPhone CHAR(10) NOT NULL,
    PermanentAddress VARCHAR2(100),
    PermanentPhone CHAR(10),
    BirthDate DATE NOT NULL,
    Sex CHAR(1) NOT NULL,
    Class VARCHAR(20) NOT NULL,
    MajorDepartment NUMBER(10),
    MinorDepartment NUMBER(10), 
    CONSTRAINT u_student_maj_dept 
    DegreeProgram VARCHAR(10) NOT NULL,
        FOREIGN KEY(MajorDepartment) 
        REFERENCES U_Department(DepartmentCode),
    CONSTRAINT u_student_min_dept 
        FOREIGN KEY(MinorDepartment) 
        REFERENCES U_Department(DepartmentCode)
);
```

```
CREATE TABLE u_course (
    CourseNumber NUMBER(15) PRIMARY KEY,
    CourseName VARCHAR2(100) NOT NULL,
    Description VARCHAR2(255) NOT NULL,
    SemesterHours NUMBER(6) NOT NULL CHECK(SemesterHours > 20),
    "Level" VARCHAR2(20) NOT NULL,
    OfferingDepartment NUMBER(10),
    CONSTRAINT offering_dept_fk 
        FOREIGN KEY(OfferingDepartment)
        REFERENCES u_department(DepartmentCode)
);
```

```
CREATE TABLE u_section (
    SectionNumber NUMBER(10),
    CourseNumber NUMBER(15),
    Instructor VARCHAR(50) NOT NULL,
    Semester VARCHAR(10) NOT NULL,
    Year NUMBER(2) NOT NULL,
    CONSTRAINT section_course_fk 
        FOREIGN KEY(CourseNumber)
        REFERENCES u_course(CourseNumber),
    CONSTRAINT section_course_pk 
        PRIMARY KEY (CourseNumber, SectionNumber)
);
```

```
CREATE TABLE u_grade (
    StudentID NUMBER(12) NOT NULL,
    SectionNumber NUMBER(10) NOT NULL,
    CourseNumber NUMBER(15) NOT NULL,
    LetterGrade CHAR(2),
    NumericGrade NUMBER(3),
    CONSTRAINT grade_student_fk 
        FOREIGN KEY (StudentID)
        REFERENCES u_student(StudentID),
    CONSTRAINT grade_section_fk 
        FOREIGN KEY (SectionNumber, CourseNumber)
        REFERENCES u_section(SectionNumber, CourseNumber),
    CONSTRAINT grade_course_st_pk 
        PRIMARY KEY (StudentID, CourseNumber, SectionNumber)
);
```
