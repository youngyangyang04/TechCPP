**1. UNION：**

- **作用**：
  - `UNION` 操作用于合并两个或多个SELECT语句的结果集，并消除重复行。
- **特点**：
  - 参与 `UNION` 操作的每个SELECT语句都必须拥有相同数量的列，且对应列的数据类型也需相似，以便可以进行合并。
  - 结果中的每一列的数据类型是由所有查询中对应列的数据类型“兼容得出”的数据类型（通常取其共同超类）。
  - 默认情况下，`UNION` 对合并结果进行去重处理（相当于执行了`DISTINCT`），只返回不重复的记录。
  - 如果想要包含所有的重复记录，可以使用 `UNION ALL`，这样可以提高查询效率，因为不需要进行去重操作。

**示例**：

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

**2. JOIN：**

- **作用**：
  - `JOIN` 操作用于根据两个表中的共同字段，将这些表中的行组合起来形成一个新的结果集。
- **特点**：
  - `JOIN` 操作可以是内连接(`INNER JOIN`)、左连接(`LEFT JOIN`)、右连接(`RIGHT JOIN`)、全连接(`FULL JOIN`)等，根据不同的需求组合表中的数据。
  - 在进行 `JOIN` 时，通常需要在 `ON` 子句中指定连接条件，即定义如何匹配来自连接表的行。
  - `JOIN` 操作不仅可以合并行，还能从两个表中选择所需的列，创建一个由这些列组成的新结果集。

**示例**：

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

总结而言，**`UNION` 主要用于垂直地合并相似结构表的数据，而 `JOIN` 主要用于水平地合并不同表中相关联的行。**二者都是数据库查询时非常有用的工具，但适用于不同的情境和需求。