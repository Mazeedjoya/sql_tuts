create database db_name;
show databases;
use db_name;
CREATE TABLE `student` ( 
 `studentid` int(10) UNSIGNED PRIMARY KEY NOT NULL AUTO_INCREMENT, 
 `name` varchar(255) , 
 `email_address` varchar(255), 
 `city` varchar(255) , 
 `fathername` varchar(255),
 `mobile` int(15)
);

show tables;
select * from student;
select name, mobile from student;
INSERT INTO student (name, email_address, city, fathername, mobile)
VALUES ('Shera' ,'sher.badnam@gmail.com', 'Merta', 'Kalam Khan',  999999999);
select * from student;

  select * from student where name  = 'Sajid' or studentid  = 2;
  select * from student where name  = 'Sajid' and studentid  = 2


@@@

select distinct name from student;

select count(*) from student;

select * from student where fathername is null;

select * from student where studentid <> 5;

select * from student where studentid < 5;

select * from student where studentid > 5;

select * from student where studentid >= 5;

select * from student where studentid <= 5;

select * from student where studentid in (1,4,7,8,10);

select * from student where email_address like '%sher';

select * from student where email_address like '%er%';

select * from student where email_address like '%gmail.com';

select * from student where email_address like '%badnam%.com';

select * from student where studentid between 5 and 8;

select * from student order by name;

select * from student order by name asc;

select * from student order by name desc;

###

select
create database
create table
where 
and, or , not 
order by 
insert into 
null values 
like 
IN, Not in 
between 
delete
drop 
count, avg, max, min, sum 
select studentid as id, name as studentname,
fathername as myfathername from student;
