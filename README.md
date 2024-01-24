To showcase the sql query, I have selected my tasks done in leetcode (for details, can refer to the attached documents):

**Q1 Employees Earning More Than Their Managers**

![image](https://github.com/kaho1156/sql/assets/98607667/d7295c3e-60bf-4a49-a62b-0fb3bc777c0d)


***** My solution:**

SELECT e.name as Employee
FROM employee AS e INNER JOIN employee AS e1 ON e.managerId = e1.id
where e.salary > e1.salary

**Q2 Department Top Three Salaries**

![image](https://github.com/kaho1156/sql/assets/98607667/a3384346-4c8b-425d-870a-3e662a60349f)


***** My solution:**

select department.name as Department, e.name as Employee, e.salary as Salary from (select departmentID, name,salary, Dense_rank() over (partition by departmentid order by salary desc) as r from employee) as e
join department on e.departmentid = department.id
where r <=3

**Q3 Delete Duplicate Emails**

![image](https://github.com/kaho1156/sql/assets/98607667/474cde27-5287-4954-adb1-f0013eb9f93f)

***** My solution:**

delete a from person a, person b where a.email = b.email and a.id > b.id

**Q4  Trips and Users**

![image](https://github.com/kaho1156/sql/assets/98607667/83d818cd-89d6-409a-a5ac-3e7cb60b8471)

***** My solution:**

select base.D as "Day", ifnull(round(cancel.c_nt/base.total_cnt,2),0) as "Cancellation Rate" from
(select  t.request_at as d, count(id) as total_cnt from Trips t join
(select * from users where role = 'client' AND banned <> "Yes") as c on t.client_id = c.users_id
join
(select * from users where role = 'driver' AND banned <> "Yes") as d on t.driver_id = d.users_id
group by t.request_at) as base
left join
(select  t.request_at as d, count(t.id) as c_nt  from Trips t
join
(select * from users where role = 'client' AND banned <> "Yes") as c on t.client_id = c.users_id
join
(select * from users where role = 'driver' AND banned <> "Yes") as d on t.driver_id = d.users_id
where t.status like '%cancelled%'
group by  t.request_at) as cancel
on base.d = cancel.d
where base.D between "2013-10-01" AND "2013-10-03"

**Q5  Find Customer Referee**

![image](https://github.com/kaho1156/sql/assets/98607667/1b7353ea-ec94-4cce-8983-04868462fb8c)

***** My solution:**

select name from customer where referee_id <> 2 or referee_id is null

**Q6  Customer Placing the Largest Number of Orders**

![image](https://github.com/kaho1156/sql/assets/98607667/6790dd43-5d96-4bba-993f-3698dfdab810)

***** My solution:**

select r.customer_number from (select customer_number,count(order_number) as cnt from orders
group by customer_number
order by count(order_number) desc) as r
limit 1

**Q7  Big Countries**

![image](https://github.com/kaho1156/sql/assets/98607667/8d92f7ac-ccd4-431b-ac86-fc59556d38d4)

***** My solution:**
select name, population, area from world 
where area >= 3000000 or population >= 25000000
