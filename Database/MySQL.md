# MySQL

## LIMIT

- 몇 개의 데이터를 보여줄지 결정한다. 

  ```mysql
  SELECT * 
  FROM Customers
  LIMIT 3;   # 위에서 3행의 데이터만 보여준다.
  ```

- 특정 행부터 시작하여 몇 개의 데이터를 보여줄지 선택할 수 있다. 처음 행은 0부터 시작한다.

  ```mysql
  SELECT Salary AS SecondHighestSalary
  FROM Employee
  ORDER BY Salary DESC
  LIMIT 2,1;   # 3번째로 높은 봉급 하나를 보여준다.
  ```

- ㅇㅇ

## Joins

```mysql
SELECT Person.FirstName, Person.LastName, Address.City, Address.State
FROM Person
LEFT JOIN Address ON Person.PersonId = Address.PersonId;
```

### INNER JOIN

![MySQL INNER JOIN](https://www.w3schools.com/MySQL/img_innerjoin.gif)

### LEFT JOIN

![MySQL LEFT JOIN](https://www.w3schools.com/MySQL/img_leftjoin.gif)

### RIGHT JOIN

![MySQL RIGHT JOIN](https://www.w3schools.com/MySQL/img_rightjoin.gif)

### CROSS JOIN

![MySQL CROSS JOIN](https://www.w3schools.com/MySQL/img_crossjoin.png)



   