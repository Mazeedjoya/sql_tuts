   ###          SQL QUERIES  ###
 1. What is the query to get all the details of a student along with the fees and result data for the student?
```
select * from student s inner join fees f
on s.stuId = f.stuId
inner join result r 
on r.stuId = s.stuId;
```
2. How can we retrieve the data of a student who has paid fees for the month of January?
```
select * from student s inner join fees f 
on s.stuId = f.stuId
where month='jan';
```
3. What is the query to get the list of all students who have not yet paid their fees?
```
select * from student s inner join fees f 
on s.stuId = f.stuId
where amount is null and month  is null;
```

4. How can we fetch the list of students who scored more than 80 marks in any subject in the result table?
```
select * from student s  join result r
on s.stuId = r.stuId
where obtainedmarks >80;
```
5. What is the query to get the details of students along with the total amount of fees they have paid so far?
```

```
6. How can we fetch the list of all students along with their fees data and result data, even if they do not have any data in the fees or result table?
```
select * from student s join fees f
on s.stuId = f.stuId
join result r 
on r.stuId = s.stuId;
```

7. What is the query to get the name, email address, and mobile number of all the students who belong to the city of "Delhi"?
```
select s.stuName , s.mobile, s.email from student s
where s.city = 'delhi';
```
8. How can we retrieve the details of students who belong to the city of "Mumbai" and have paid their fees for the month of February?
```
select * from student s
join fees f on 
s.stuId = f.stuId
where s.city ='jaipur' and f.month ='feb' and f.amount is not null;
```

9. What is the query to get the name, email address, and total amount of fees paid by all the students who have paid their fees?
```
select s.stuName , s.email, sum(f.amount) from student s join 
fees f on s.stuId = f.stuId
where f.amount is not null
group by s.stuName, s.email;
```

10. How can we fetch the details of all students who have taken any test before a specific date?
```
select * from  student s join result r 
on s.stuId = r.stuId
where r.subject is not null and testdate > 2022-04-23;
```

11. What is the query to get the name, email address, and subject name of all the students who have scored more than 90 marks in any subject?
```
select s.stuName , s.email, r.obtainedmarks, r.subject from student s join 
result r on s.stuId = r.stuId
where r.obtainedmarks >90;
```
12. How can we retrieve the details of students who belong to the city of "Bangalore" and have scored less than 50 marks in any subject?
```
select * from student s join 
result r on s.stuId = r.stuId
where r.obtainedmarks > 50 and s.city = 'BAngalore';
```
13. What is the query to get the details of all students along with their fees and result data, sorted by their name in ascending order?
```
select * from student s join fees f
on s.stuId = f.stuId
join result r 
on r.stuId = s.stuId
order by s.stuName asc;
```

14. How can we fetch the name, email address, and total amount of fees paid by all the students who have not paid their fees yet?
```
####
```
15. What is the query to get the details of all students who have paid their fees for the month of March and have scored more than 70 marks in any subject?
```
select * from student s join fees f
on s.stuId = f.stuId
join result r 
on r.stuId = s.stuId
where f.amount is not null
 and f.month='march'
 and r.obtainedmarks >70;
 ```

16. How can we retrieve the details of students who have not taken any test yet?
```
select * from student s left join
 result r on s.stuId = r.stuId
 where r.subject is null;
 ```

17. What is the query to get the name, email address, and subject name of all the students who have scored less than 40 marks in any subject?
```
select s.stuName,  s.email, r.subject from student s join fees f
on s.stuId = f.stuId
join result r 
on r.stuId = s.stuId
where r.obtainedmarks< 70;
```
18. How can we fetch the details of students who belong to the city of "Pune" and have paid their fees for the month of January?
```
select * from student s inner join fees f
on s.stuId = f.stuId
join result r 
on r.stuId = s.stuId
where s.city= 'jaipur'
and f.month = 'jan'
and f.amount is not null;
```


19. What is the query to get the name, email address, and mobile number of all the students who have not taken any test yet?
```
select s.stuName , s.email, s.mobile from student s left join
 result r on s.stuId = r.stuId
 where r.subject is null;
 ```

20. How can we retrieve the details of students who have scored more than 60 marks in all the subjects they have taken tests for?
 ```
 select * from student s join result r 
  on s.stuId = r.stuId
  where r.obtainedmarks >60;
  ```
