 # INSTITUTE MANAGEMENT 
 
 ## CREATE DATABASE.
```
create database institutemanagement;
```
## USE DATABASE.
```
use institutemanagement;
```

## STUDENT TABLE .
```
create table student (	
id integer auto_increment primary key ,
name varchar(40) not null , 
father_name varchar(40) not null,
mobile bigint, 
email varchar(40) unique not null,
admissionDate date
);
```
## ADDRESS TABLE.
```
create table address(		
add_id integer auto_increment primary key,
stuId integer not null,
city varchar(30) not null,
state varchar(30) not null ,
pincode integer not null,
colony varchar(40),
house_no integer ,
landline_no bigint not null,
foreign key(stuId) references student(id)	
); 
```

## EMPLOYEE TABLE.
```
create table employee(	
id integer auto_increment primary key,
emp_name varchar(40) not null,
emp_type integer  not null ,
email varchar(40) unique not null,
phone bigint ,
foreign key (emp_type) references employee_type(id)
);
```
## EMPLOYEE TYPE TABLE. 
```
create table employee_type(		
id integer auto_increment not null primary key,
emp_type varchar(20)
);
```

## COURSE TABLE.
```
create table course(	
id integer auto_increment primary key not null,
course_name varchar(25) not null,
course_fee integer not null,
startDate date not null,
endDate date not null,
timing time );
```

## TEST TABLE.
```
create table test (	
id integer auto_increment primary key,
test_name varchar(40) not null ,
passing_marks integer not null ,
total_marks integer not null ,
date date not null );
```

## RESULT TABLE. 
```
create table result ( 		
id integer auto_increment not null primary key,
test_Id integer not null,
stu_Id integer not null ,
obtainedmarks int not null,
result enum('pass' , 'fail'),
foreign key (stu_Id) references student(id),
foreign key (test_Id) references test(id) );
```
 
 ## FEES TABLE.
 ```
 create table fees(		
 id integer auto_increment not null primary key,
 stuId integer not null,
 amount integer  not null ,
 depositDate date not null ,
 foreign key (stuId) references student(id)
 );
 ```
 
 ## SALARY TABLE. 
 ```
 create table salary (		
 id integer not null auto_increment primary key,
 emp_id integer not null ,
 amount integer not null ,
 date date not null,
 foreign key (emp_id) references employee(id) 
 );
 ```
 
 ## STUDENT COURSE TABLE.
 ```
 create table  student_course(		
 id integer auto_increment not null primary key,
 stuId integer not null ,
 courseId integer not null,
 foreign key (stuId) references student(id),
 foreign key (courseId) references course(id)
 );
 ```
 
 ## EXPENSE DETAIL TABLE.
 ```
 create table expenses (		-- 11
 id integer auto_increment not null primary key,
 exp_detail varchar (255) not null ,
 amount integer  not null,
 expense_date date not null );
 ```
 
 
