To showcase the sql query, I have selected my tasks done in leetcode (for details, can refer to the attached documents):

Q1 Employees Earning More Than Their Managers

![image](https://github.com/kaho1156/sql/assets/98607667/d7295c3e-60bf-4a49-a62b-0fb3bc777c0d)


*** My solution:

SELECT e.name as Employee
FROM employee AS e INNER JOIN employee AS e1 ON e.managerId = e1.id
where e.salary > e1.salary

![image](https://github.com/kaho1156/sql/assets/98607667/860f6614-abe2-4573-ab7a-1ec1ed307daa)


