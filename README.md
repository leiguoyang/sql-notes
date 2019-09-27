# SQL notes
About getting data, setting data and table relationships.

## Table of content
- [Getting data](#getting-data)
  - [Select](#select)
  - [Alias](#alias)
  - [Where](#where)
  - [Condition](#condition)
  - [Joins](#joins)
  - [Order by](#order-by)
  - [Limit](#limit)
  - [Group by](#group-by)
  - [Having](#having)
  - [Union](#union)
  - [With clause](#with-clause)
  - [Calculated field](#calculated-field)
  - [Function](#function)
  - [Subquery](#subquery)
  - [Case when](#case-when)
- [Setting data](#setting-data)
- [View](#view)
- [SQLite](#sqlite)
- [Comment](#comment)

## Getting data

### Select
Select用来获取表中的栏, 如获取所有的栏。

```
SELECT *
FROM table_name;
```

获取特定的栏。
```
SELECT column_name
FROM table_name;
```

### Alias
可以对表中的某一栏定义一个别名，或对一个表定义一个别名。

```
SELECT column_name AS alias_name
FROM table_name;
```

```
SELECT column_name
FROM table_name AS alias_name;
```

也可以不用`AS`来定义alias，这两者没有区别，只是`AS`是一种explicit的方式。

```
SELECT column_name
FROM table_name alias_name;
```

column alias 不可用于calculated field, `WHERE`和`GROUP BY`，否则会报错。如下例子

```
SELECT Customers.CustomerName, COUNT(Orders.OrderID) AS Orders_qty,
CASE
WHEN Orders_qty >= 5 THEN 'high'
ELSE 'low' END AS Priority
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID=Orders.CustomerID
GROUP BY Customers.CustomerName
ORDER BY Orders_qty DESC;
```

`Error 1: could not prepare statement (1 no such column: Orders_qty)`.正确为

```
SELECT Customers.CustomerName, COUNT(Orders.OrderID) AS Orders_qty,
CASE
WHEN COUNT(Orders.OrderID) >= 5 THEN 'high'
ELSE 'low' END AS Priority
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID=Orders.CustomerID
GROUP BY Customers.CustomerName
ORDER BY Orders_qty DESC;
```

但可用于`ORDER BY`.这和SQL的运行顺序有关。SQL的运行顺序如下：

1. FROM clause
2. WHERE clause
3. GROUP BY clause
4. HAVING clause
5. SELECT clause
6. ORDER BY clause

### Where
Where用来选取符合特定条件的数据。

```
SELECT column_name
FROM table_name
WHERE column_name = value;
```

### Condition
And, or, between, not, in, like, >, >=, <, <=, =, !=

### Joins
Joins可以通过primary key和foreign key将多个表进行关联而得到新的result set. Joins的类型有inner join和outer join。

```
SELECT table_a.column_01, table_b_column_01
FROM table_a
INNER JOIN table_b
ON table_a.column_03 = table_b.column_03;
```

各类型的Join返回的是

- `INNER JOIN` Returns all rows when there is at least one match in BOTH tables. `INNER JOIN` is the same as `JOIN`
- `LEFT JOIN` Return all rows from the left table, and the matched rows from the right table.
- `RIGHT JOIN` Return all rows from the right table, and the matched rows from the left table.
- `FULL JOIN` Return all rows when there is a match in ONE of the tables.

### Order by
Order by用来对数据依据其中一栏或多栏的大小进行排序，如升序或降序，默认是升序。

```
SELECT column_name
FROM table_name
ORDER BY column_name;
```

或依据多个栏进行排序, 先写的栏位会先排序。

```
SELECT column_name
FROM table_name
ORDER BY column_name_one, column_name_two;
```

如果上面的例子需要一个升序，一个降序，则可以这样写。

```
SELECT column_name
FROM table_name
ORDER BY column_name_one ASC, column_name_two DESC;
```

### Limit
Limit用来限定输出的record数量。

### Group by
Group by对数据进行分类汇总。

```
SELECT COUNT(column_name_01)
FROM table_name
GROUP BY column_name_02;
```

Group by多栏其实就是对同时满足多个条件的rows进行分类汇总。

假如有如下的数据

```
Table: Subject_Selection

Subject   Semester   Attendee
---------------------------------
ITB001    1          John
ITB001    1          Bob
ITB001    1          Mickey
ITB001    2          Jenny
ITB001    2          James
MKB114    1          John
MKB114    1          Erica
```

我想看每个学期每个课程的参与人数，那就可以query如下

```
SELECT Subject, Semester, COUNT(Attendee)
FROM Subject_Selection
GROUP BY Subject, Semester
```

### Having
Having就是对汇总的数据进一步筛选。The `having` command is used instead of `where` with aggregate function.

```
SELECT COUNT(column_name)
FROM table_name
HAVING COUNT(column_name) > value;
```

### Union
Union对多个表进行merge. UNION selects only distinct values. Use UNION ALL to also select duplicate values.

Notice that each SELECT statement within the UNION must

- Have the same number of columns.
- The columns must also have similar data types.
- Also, the columns in each SELECT statement must be in the same order.

```
SELECT column_name FROM table_a
UNION
SELECT column_name FROM table_b;
```

The column names in the result-set of a UNION are usually equal to the column names in the first SELECT statement in the UNION.

`UNION ALL`

```
SELECT column_name FROM table_a
UNION ALL
SELECT column_name FROM table_b;
```

### With clause

The SQL `WITH` clause allows you to give a sub-query block a name, which can be referenced in several places within the main SQL query. 

```
WITH employee AS (SELECT * FROM Employees)
SELECT * FROM employee WHERE ID < 20
UNION ALL
SELECT * FROM employee WHERE Sex = 'M'
```


### Calculated field

```
SELECT name, price, quantity, price * quantity AS total FROM order_details;
```

其中，`price * quantity AS total`是calculated field.

如你的table里有`first name`和`last name`, 你可以做个`full name`作为calculated field.

### Function

### Subquery

下面的query是Finds employees whose salary is greater than the average salary of all employees.

```
SELECT employees_id, first_name, salary
FROM emmployees
WHERE salary > (SELECT AVG(salary) FROM emmployees) ;
```

其中，`SELECT AVG(salary) FROM emmployees`是一个subquery.

### Case when

```
CASE WHEN conditional THEN returned_value_01
WHEN conditional THEN returned_value_02
ELSE returned_value_03
END
```

or

```
CASE WHEN conditional THEN returned_value_01
WHEN conditional THEN returned_value_02
ELSE returned_value_03
END AS alias_name
```

## Setting data
- Insert a new record
- Update
- Delete (a record, a table)
- Create a table, create a database
- Insert a new column
- Modify table name, and column name

## Views

## Tables relationships
- one to one
- one to many
- many to many

## SQLite
- `sqlite3 [file_name]` 打开sqlite文件

## Comment
One line comment

```
-- comments comes here
```

Block comment

```
/* comment comes here */
```
