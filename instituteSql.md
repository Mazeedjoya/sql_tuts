 
 ## create database institute_management;
 ```
 use institute_management;
 ```
 
## Student 
```
 create table student (	
stuId integer auto_increment primary key ,
name varchar(40) not null , 
father_name varchar(40) not null,
mobile bigint, 
email varchar(40) unique not null,
admissionDate date
);
```
## Address
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
foreign key(stuId) references student(stuId)	
); 
```
## Employee
```
 create table employee(	
empId integer auto_increment primary key,
emp_name varchar(40) not null,
emp_type integer  not null ,
email varchar(40) unique not null,
phone bigint ,
foreign key (emp_type) references employee_type(emptypeId)
);
```
## Employee Type
```
 create table employee_type(		
emptypeId integer auto_increment not null ,
emp_type varchar(20),
primary key(emptypeId )
);
```
## Course
```
create table course(	
courseId integer auto_increment primary key not null,
course_name varchar(25) not null,
course_fee integer not null,
startDate date not null,
endDate date not null,
timing time );
```
## Test
```
create table test (	
testId integer auto_increment primary key,
test_name varchar(40) not null ,
passing_marks integer not null ,
total_marks integer not null ,
date date not null );
```
## Result
```
create table result ( 		
resId integer auto_increment not null primary key,
testId integer not null,
stuId integer not null ,
obtainedmarks int not null,
result enum('pass' , 'fail'),
foreign key (stuId) references student(stuId),
foreign key (testId) references test(testId) );
```
## Fees
```
create table fees(		
feeId integer auto_increment not null primary key,
stuId integer not null,
amount integer  not null ,
depositDate date not null ,
foreign key (stuId) references student(stuId)
);
```
## Salary
```
create table salary (		
salId integer not null auto_increment primary key,
empId integer not null ,
amount integer not null ,
recieveDate date not null,
foreign key (empId) references employee(empId) 
);
```
## Student Course
```
create table  student_course(		
stucoId integer auto_increment not null primary key,
stuId integer not null ,
courseId integer not null,
foreign key (stuId) references student(stuId),
foreign key (courseId) references course(courseId)
);
```
## Expenses
```
create table expenses (  id integer auto_increment not null primary key,
 exp_detail varchar (255) not null ,
 amount integer  not null, expense_date date not null );
```
# QUESTIONS 



### QUESTIONS AND ANSWERS

1. Name of all students jinhone abi tak koi fees deposit ni ki --
```
select * from student where stuId not in (select stuId from fees); 
```


2. Sbse jyada fees kis student ne di hai. naam btao --
```
select name , stuId from student
 where stuId in(select stuId from fees
  where amount = (select max(amount) from fees) );
```
3. Sbse jyada fees me 2nd number pr jo student hai uska naam btao 
```
select name , stuId from student where
 stuId in(select stuId from fees where
 amount = (select max(amount) from fees 
 where amount  != (select max(amount) from fees)) );
```
4. Coaching me total kitne employees hain unka naam and designation/role show krvao
```

  select e.empId,e.emp_name , etype.emp_type from employee e
 join employee_type etype on e.emp_type = etype.emptypeId; 

```
5. Kis employee ne kitni salary uthayi hai ab tak vo btao ya month wise --
```
select e.emp_name ,etype.emp_type ,sum(s.amount), count(s.salId) from employee  e join employee_type etype on e.emp_type = etype.emptypeId
join salary s on s.salId = e.empId where recieveDate between '2023-02-01' and '2023-02-27'   group by e.emp_name ,etype.emp_type ,s.amount ;
 
```
select emp.emp_name ,et.emp_type sum(s.amount) from employee join employee_type on emp.id = et.id
join salary s on s.id = emp.id group by emp.emp_name ,et.emp_type s.amount;

6. Vo sare students jo abi tak 1 b test me fail hue hai unka naam, subject, 
totalmarks, passingmarks, obtainedmarks btao  
```
select s.name , r.obtainedmarks , t.total_marks , t.passing_marks , t.test_name , c.course_name , r.result
from student s join result r on s.id =r.stu_Id  
join course c on c.id = r.stu_Id 
join test t on t.id = c.id 
where  r.result = 'fail';  
```
select s.name  from student s join result r on s.id =r.stu_Id 
join course c on c.id = r.stu_Id 
join test t on t.id = c.id

7. Particular month ka kharcha btao. Kharche me tume salary and expenses dono add krne hai 
```

```
8. Particular month me total income btao 
```
select  sum(amount) from fees where depositDate between '2023-03-01' and '2023-03-31'   ;
```
9. Total income aaj tak 
```
select sum(amount) from fees;
```
10. Total kharche aaj tak 
```
select sum(amount) from expenses;
```
11. Kis course me kitne students hai vo btane hai  
     coursename startdate time totalstudents
```
SELECT  c.course_name, c.startDate, c.timing, COUNT(sc.courseId) FROM   
  student s JOIN student_course sc ON s.stuId = sc.stuId      
  JOIN   course c ON c.courseId = sc.courseId  WHERE  
  sc.courseId IN (SELECT   courseId   FROM   course   WHERE   course_name = 'Nodejs') 
  GROUP BY sc.courseId , c.course_name , c.startDate , c.timing ;
```

12. Vo course btana hai jisme sbse jyada income hui hai 
```
```
13. Vo course btana hai jisme sbse kam income hui hai 
```
```
14. Kaunsa course hai jisme sbse jyada students hai 
```
select  c.course_name as courseName , count(sc.stuId) as stuCount from course c join 
student_course sc on  c.courseId = sc.courseId group by c.course_name limit 1 ;

```
15. Kaunsa course hai jisme sbse kam students hain
  
```
```
................
 
1. Kaunsa course hai jisme koi admission ni hua hai.
```
select * from course where courseId not in (select courseId from student_course);
```
2. Sbse jyada expense from expense table kis chiz ke liye hua hai 
```
select amount, exp_detail from expenses where amount =(select max(amount ) from expenses);
```
3. Employee list print krvani hai unki total paid salary ke descending order me
Sajid Teacher 100000
Shahrukh Teacher 80000
Rehna Peon 20000
```
select e.emp_name , sum(s.amount) from employee e join salary s on e.empId = s.empId 
group by e.emp_name , s.amount order by amount desc;
```
4. Course table ko alter krna hai aur usme ek teacherid column add krna hai jo ki foreign key hogi 
```
alter table course add column teacherId integer ;
alter table course add foreign key(teacherId) references employee(empId);
```
5. Kaunse course me kaunsa teacher pdhata hai uski detail print krvani hai 
CourseName CourseTime TeacherName

```
select e.emp_name ,c.course_name , c.timing  from course c join employee e on c.teacherId = e.empId;
  
```
6. Student list print krvani hai unki total paid fees ke descending order me
Sajid Nodejs 100000
Shahrukh JavaScript 80000
Rehna HTML 20000
```
select s.name , sum(f.amount) from student s  join fees f on s.stuId = f.stuId 
group by s.name , f.amount order by amount desc; -- 18
```

7. Kisi b year ka total profit/loss btana hai
Total fees - (total salary + total expenses)
```
select ((select sum(amount) as total from fees)  - (select sum(amount) from expenses) +(select sum(amount) from salary));
```
8. Student count list print krvani hai unki total batch count ke descending order me
Nodejs 10:00PM 10/01/2023  10/07/2023 30
JS 9:00PM 10/01/2023  10/07/2023 20
HTML 10:00AM 10/01/2023  10/07/2023 40
```
select c.course_name , c.startDate, c.endDate , c.timing , count(sc.stuId) 
from course c join student_course sc on c.courseId = sc.courseId 
group by c.course_name , c.startDate, c.endDate , c.timing ;
```

9. Student list print krvani hai unki total student in pincode ke descending order me
302012 Jhotwara 20
303012 Merta 15
304013 Sikar 12
```
select city ,pincode ,count(*) from address group by city , pincode;
```
-- select empname from emp where count()
10. Ek view bnana hai. 
StudentName Mobie Email CourserName CourseStartDate CourseEndDate Time
 TotalFees AvgMarks Address(plotno, colony, city, state, pincode)
```
create view studentData(
name , mobile , email,coursename , startDate , endDate , timing , totalamount , avgmarks , city , pincode)  as 
 select s.name , s.mobile ,s.email , c.course_name , c.startDate , c.endDate ,
 c.timing ,sum(f.amount), avg(r.obtainedmarks) , ad.city , ad.pincode
 from  result r  join address ad  on r.stuId = ad.stuId join  fees f  on ad.stuId = f.stuId join 
 student s on f.stuId = s.stuId join  student_course sc  on s.stuId = sc.stuId  join course c  on sc.courseId = c.courseId  
 group by 
 s.name , s.mobile ,s.email , c.course_name , c.startDate , c.endDate ,
 c.timing  , ad.city , ad.pincode; 
```
11. Ek view result pr bnana hai 
StudentName Mobile TotalMakrs TotalOBtainedMarks Avg Rank
Sajid 945655445 500 400 80 1 
```
```
12. Vo student jinhone koi b fees jama ni krayi hai unko delete kr dena hai student table se 
Aur iske child records Address, Result tables me hai vo vha se b delete krna hai 
```
```
13. Expenses table se monthly expenses descending order me btane hai 
Year Month TotalExpenses
2023 Feb 25000
2022 Dec 12000
```
  select expense_date ,exp_detail , amount from expenses order by expense_date desc;
```
14. Kaunse teacher ke batch ke students ki performance sbse best hai 
```
```
15. ek view bnana hai 
TeacherName Designation BatchName BatchStartDate BatchEndDate  TotalFeesDepositByThisBatch  TotalSalary
```
```

