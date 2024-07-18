# MySQL #

### SELECT ###
The SELECT statement is used to select data from a database

```sql
SELECT column1, column2, ... FROM table_name;
```

Used to select all columns
```sql
SELECT * FROM table_name;
```

Used to return only distinct (different) values
```sql
SELECT DISTINCT column1, column2, ... FROM table_name;
```

### WHERE ###
The WHERE clause is used to filter records

```sql
SELECT column1, column2, ... FROM table_name WHERE condition;
```

Equal
```sql
SELECT * FROM Customers WHERE Country = 'Mexico';
SELECT * FROM Customers WHERE CustomerID = 1;
```

Greater than
```sql
SELECT * FROM Products WHERE Price > 30;
```

Less than
```sql
SELECT * FROM Products WHERE Price < 30;
```

Greater than or equal
```sql
SELECT * FROM Products WHERE Price >= 30;
```

Less than or equal
```sql
SELECT * FROM Products WHERE Price <= 30;
```

Not equal
```sql
SELECT * FROM Products WHERE Price <> 30;
```

Between a certain page
```sql
SELECT * FROM Product WHERE Price BETWEEN 50 AND 60;
```

Search for a pattern
```sql
SELECT * FROM Customers WHERE City LIKE 's%';
```

To specify multiple possible values for a column
```sql
SELECT * FROM Customers WHERE City IN ('Paris','London');
```

### AND, OR, NOT ###
The AND operator displays a record if all the conditions separated by AND are TRUE

```sql
SELECT column1, column2, ... FROM table_name WHERE condition1 AND condition2 AND condition3 ...;
SELECT * FROM Customers WHERE Country = 'Germany' AND City = 'Berlin';
```

The OR operator displays a record if any of the conditions separated by OR is TRUE
```sql
SELECT column1, column2, ... FROM table_name WHERE condition1 OR condition2 OR condition3 ...;
SELECT * FROM Customers WHERE Country = 'Germany' OR City = 'Berlin';
```

The NOT operator displays a record if the condition(s) is NOT TRUE
```sql
SELECT column1, column2, ... FROM table_name WHERE NOT condition;
SELECT * FROM Customers WHERE NOT Country = 'Germany';
```

#### Combining AND, OR and NOT ####
```sql
SELECT * FROM Customers WHERE Country = 'Germany' AND (City = 'Berlin' OR City = 'Stuttgart');
SELECT * FROM Customers WHERE NOT Country = 'Germany' AND NOT Country = 'USA';
```

### ORDER BY ###
The ORDER BY keyword is used to sort the result-set in ascending or descending order

```sql
SELECT column1, column2, ... FROM table_name ORDER BY column1, column2, ... ASC|DESC;
SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC; 
```

### INSERT INTO ###
The INSERT INTO statement is used to insert new records in a table

Specify both the column names and the values to be inserted
```sql
INSERT INTO table_name (column1, column2, column3, ...) VALUES (value1, value2, value3, ...);
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country) VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```

Adding values for all the columns of the table
```sql
INSERT INTO table_name VALUES (value1, value2, value3, ...);
INSERT INTO Customers (CustomerName, City, Country) VALUES ('Cardinal', 'Stavanger', 'Norway');
```

### NULL Values ###
A field with a NULL value is a field with no value

Test for NULL Values
```sql
SELECT column_names FROM table_name WHERE column_name IS NULL;
SELECT column_names FROM table_name WHERE column_name IS NOT NULL;

SELECT CustomerName, ContactName, Address FROM Customers WHERE Address IS NULL;
SELECT CustomerName, ContactName, Address FROM Customers WHERE Address IS NOT NULL;
```

### UPDATE ###
The UPDATE statement is used to modify the existing records in a table

```sql
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
UPDATE Customers SET ContactName = 'Alfred Schmidt', City = 'Frankfurt' WHERE CustomerID = 1;
UPDATE Customers SET PostalCode = 00000 WHERE Country = 'Mexico';
```

### DELETE ###
The DELETE statement is used to delete existing records in a table

```sql
DELETE FROM table_name WHERE condition;
DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';
```

Delete all records
```sql
DELETE FROM table_name;
DELETE FROM Customers;
```

### LIMIT ###
The LIMIT clause is used to specify the number of records to return

```sql
SELECT column_name(s) FROM table_name WHERE condition LIMIT number;
SELECT * FROM Customers LIMIT 3;
```

The SQL query below says "return only 3 records, start on record 4 (OFFSET 3)"
```sql
SELECT * FROM Customers LIMIT 3 OFFSET 3;
```

Add a WHERE clause
```sql
SELECT * FROM Customers WHERE Country='Germany' LIMIT 3;
```

### MIN() AND MAX() ###
The MIN() function returns the smallest value of the selected column

The MAX() function returns the largest value of the selected column

```sql
SELECT MIN(column_name) FROM table_name WHERE condition;
SELECT MAX(column_name) FROM table_name WHERE condition;

SELECT MIN(Price) AS SmallestPrice FROM Products;
SELECT MAX(Price) AS LargestPrice FROM Products;
```