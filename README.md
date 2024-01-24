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
