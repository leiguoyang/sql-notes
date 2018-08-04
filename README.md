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
FROM table_name
```

获取特定的栏。
```
SELECT column_name
FROM table_name
```

### Alias
可以对表中的某一栏定义一个别名，或对一个表定义一个别名。

```
SELECT column_name AS alias_name
FROM table_name

```

```
SELECT column_name
FROM table_name AS alias_name
```

### Where
Where用来选取符合特定条件的数据。

```
SELECT column_name
FROM table_name
WHERE column_name = value
```

### Condition
And, or, between, not, in, like, >, >=, <, <=, =, !=

### Joins

### Order by
Order by用来对数据依据其中一栏或多栏的大小进行排序，如升序或降序，默认是升序。

```
SELECT column_name
FROM table_name
ORDER BY column_name
```

或依据多个栏进行排序, 先写的栏位会先排序。

```
SELECT column_name
FROM table_name
ORDER BY column_name_one, column_name_two
```

如果上面的例子需要一个升序，一个降序，则可以这样写。

```
SELECT column_name
FROM table_name
ORDER BY column_name_one ASC, column_name_two DESC
```

### Limit
Limit用来限定输出的record数量。

### Group by
Group by对数据进行分类汇总。

### Having
Having就是对汇总的数据进一步筛选。

```
SELECT COUNT(column_name)
FROM table_name
HAVING COUNT(column_name) > value;
```

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
