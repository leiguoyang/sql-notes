# SQL notes
About getting data, setting data and table relationships.

## Getting data
- Select (select some columns from the table; and calculated fields?)
- Alias (column alias, table alias)
- Joins (Inner join, left join and self join)
- Order (Ascending order and descending order)
- Limit (limit the amount of record returned)
- Group by
- Having
- Function (aggregate function and scalar function

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
