# SQL Commands #

Command  | Syntax
------------- | -------------
SELECT | SELECT column1, column2, ... FROM table_name;
SELECT | SELECT * FROM table_name;
SELECT | SELECT DISTINCT column1, column2, ... FROM table_name;
WHERE  | SELECT column1, column2, ... FROM table_name WHERE condition;
WHERE  | SELECT * FROM Customers WHERE Country = 'Mexico';
WHERE  | SELECT * FROM Customers WHERE CustomerID = 1;
WHERE  | SELECT * FROM Products WHERE Price > 30;
WHERE  | SELECT * FROM Products WHERE Price < 30;
WHERE  | SELECT * FROM Products WHERE Price >= 30;
WHERE  | SELECT * FROM Products WHERE Price <= 30;
WHERE  | SELECT * FROM Products WHERE Price <> 30;
WHERE  | SELECT * FROM Product WHERE Price BETWEEN 50 AND 60;
WHERE  | SELECT * FROM Customers WHERE City LIKE 's%';
WHERE  | SELECT * FROM Customers WHERE City IN ('Paris','London');
AND    | SELECT column1, column2, ... FROM table_name WHERE condition1 AND condition2 ...;
AND    | SELECT * FROM Customers WHERE Country = 'Germany' AND City = 'Berlin';
OR     | SELECT column1, column2, ... FROM table_name WHERE condition1 OR condition2 ...;
OR     | SELECT * FROM Customers WHERE Country = 'Germany' OR City = 'Berlin';
NOT TRUE | SELECT column1, column2, ... FROM table_name WHERE NOT condition;
NOT TRUE | SELECT * FROM Customers WHERE NOT Country = 'Germany';
AND, OR and NOT | SELECT * FROM Customers WHERE Country = 'Germany' AND (City = 'Berlin' OR City = 'Stuttgart');
AND, OR and NOT | SELECT * FROM Customers WHERE NOT Country = 'Germany' AND NOT Country = 'USA';
ORDER BY | SELECT column1, column2, ... FROM table_name ORDER BY column1, column2, ... ASC|DESC;
ORDER BY | SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC;
INSERT INTO | INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
INSERT INTO | INSERT INTO Customers (CustomerName, ContactName, Address) VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21');
INSERT INTO | INSERT INTO table_name VALUES (value1, value2, value3, ...);
INSERT INTO | INSERT INTO Customers (CustomerName, City, Country) VALUES ('Cardinal', 'Stavanger', 'Norway');
NULL VALUES | SELECT column_names FROM table_name WHERE column_name IS NULL;
NULL VALUES | SELECT column_names FROM table_name WHERE column_name IS NOT NULL;
NULL VALUES | SELECT CustomerName, ContactName, Address FROM Customers WHERE Address IS NULL;
NULL VALUES | SELECT CustomerName, ContactName, Address FROM Customers WHERE Address IS NOT NULL;
UPDATE  | UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
UPDATE  | UPDATE Customers SET ContactName = 'Alfred Schmidt', City = 'Frankfurt' WHERE CustomerID = 1;
UPDATE  | UPDATE Customers SET PostalCode = 00000 WHERE Country = 'Mexico';
DELETE  | DELETE FROM table_name WHERE condition;
DELETE  | DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';
DELETE ALL | DELETE FROM table_name;
DELETE ALL | DELETE FROM Customers;
LIMIT | SELECT column_name(s) FROM table_name WHERE condition LIMIT number;
LIMIT | SELECT * FROM Customers LIMIT 3;
LIMIT | SELECT * FROM Customers WHERE Country='Germany' LIMIT 3;
MIN() | SELECT MIN(column_name) FROM table_name WHERE condition;
MIN() | SELECT MIN(Price) AS SmallestPrice FROM Products;
MAX() | SELECT MAX(column_name) FROM table_name WHERE condition;
MAX() | SELECT MAX(Price) AS LargestPrice FROM Products;


### COUNT(), AVG(), SUM() ###
The COUNT() function returns the number of rows that matches a specified criterion

```sql
SELECT COUNT(column_name) FROM table_name WHERE condition;
SELECT COUNT(ProductID) FROM Products;
```
*NULL values are not counted*

The AVG() function returns the average value of a numeric column
```sql
SELECT AVG(column_name) FROM table_name WHERE condition;
SELECT AVG(Price) FROM Products;
```
*NULL values are ignored*

The SUM() function returns the total sum of a numeric column
```sql
SELECT SUM(column_name) FROM table_name WHERE condition;
SELECT SUM(Quantity) FROM OrderDetails;
```
*NULL values are ignored*

### LIKE ###
* The LIKE operator is used in a WHERE clause to search for a specified pattern in a column
* There are two wildcards often used in conjunction with the LIKE operator:
  * The percent sign (%) represents zero, one, or multiple characters
  * The underscore sign (_) represents one, single character

```sql
SELECT column1, column2, ... FROM table_name WHERE column LIKE pattern;
```

LIKE Operator  | Description
------------- | -------------
WHERE CustomerName LIKE 'a%'    | Finds any values that start with "a"
WHERE CustomerName LIKE '%a'  | Finds any values that end with "a"
WHERE CustomerName LIKE '%or%' | Finds any values that have "or" in any position
WHERE CustomerName LIKE '_r%' | Finds any values that have "r" in the second position
WHERE CustomerName LIKE 'a_%' | Finds any values that start with "a" and are at least 2 characters in length
WHERE CustomerName LIKE 'a__%' | Finds any values that start with "a" and are at least 3 characters in length
WHERE CustomerName LIKE 'a%o' | Finds any values that start with "a" and ends with "o"

### IN ###
* The IN operator allows you to specify multiple values in a WHERE clause
* The IN operator is a shorthand for multiple OR conditions

```sql
SELECT column_name(s) FROM table_name WHERE column_name IN (value1, value2, ...);
SELECT column_name(s) FROM table_name WHERE column_name IN (SELECT STATEMENT);

SELECT * FROM Customers WHERE Country IN ('Germany', 'France', 'UK');
SELECT * FROM Customers WHERE Country NOT IN ('Germany', 'France', 'UK');
SELECT * FROM Customers WHERE Country IN (SELECT Country FROM Suppliers);
```

### BETWEEN ###
* The BETWEEN operator selects values within a given range
* The values can be numbers, text, or dates
* The BETWEEN operator is inclusive: begin and end values are included

```sql
SELECT column_name(s) FROM table_name WHERE column_name BETWEEN value1 AND value2;

SELECT * FROM Products WHERE Price BETWEEN 10 AND 20;
SELECT * FROM Products WHERE Price NOT BETWEEN 10 AND 20;
SELECT * FROM Products WHERE Price BETWEEN 10 AND 20 AND CategoryID NOT IN (1,2,3);
SELECT * FROM Products WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni' ORDER BY ProductName;
SELECT * FROM Products WHERE ProductName NOT BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni' ORDER BY ProductName;
SELECT * FROM Orders WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';
```

### Aliases ###
* Aliases are used to give a table, or a column in a table, a temporary name
* Aliases are often used to make column names more readable
* An alias only exists for the duration of that query
* An alias is created with the AS keyword.

Alias Column Syntax
```sql
SELECT column_name AS alias_name FROM table_name;

SELECT CustomerName AS Customer, ContactName AS "Contact Person" FROM Customers;
SELECT CustomerName, CONCAT_WS(', ', Address, PostalCode, City, Country) AS Address FROM Customers;
```

Alias Table Syntax
```sql
SELECT column_name(s) FROM table_name AS alias_name;

SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;

SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName
FROM Customers, Orders
WHERE Customers.CustomerName='Around the Horn' AND Customers.CustomerID=Orders.CustomerID;
```

### Joins ###
* A JOIN clause is used to combine rows from two or more tables, based on a related column between them
* INNER JOIN: Returns records that have matching values in both tables
* LEFT JOIN: Returns all records from the left table, and the matched records from the right table
* RIGHT JOIN: Returns all records from the right table, and the matched records from the left table
* CROSS JOIN: Returns all records from both tables

![image](https://github.com/user-attachments/assets/47d07018-3d5d-476c-be79-b7ccadc13d23)

#### INNER JOIN ####
```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;

SELECT Orders.OrderID, Customers.CustomerName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

#### LEFT JOIN ####
```sql
```

## LeetCode ##

### 1. Combine Two Tables ###
```sql
SELECT firstName, lastName, city, state
FROM Person p
LEFT JOIN Address a
ON p.personId = a.personId
```

![image](https://github.com/user-attachments/assets/720629d6-da68-46b3-9e2e-27d8e4e1fd1e)

### 2. Employees Earning More Than Their Managers ###
```sql
SELECT e2.name AS Employee 
FROM employee e1
INNER JOIN employee e2 ON e1.id = e2.managerID
WHERE e1.salary < e2.salary;
```
![image](https://github.com/user-attachments/assets/b5c497a6-1461-44a3-a035-78fa91dbd98f)


Source:
* https://www.w3schools.com/mysql
