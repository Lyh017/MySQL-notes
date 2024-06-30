## DQL介绍

* DQL是Data Query Language(数据查询语言)，用来查询数据库中表的记录
* 查询关键字 SELECT

### DQL-语法
```SQL
SELECT 
    字段列表
FROM
    表名列表
WHERE
    条件列表
GROUP BY
    分组字段列表
HAVING 
    分组后条件列表
ORDER BY
    排序字段列表
LIMIT
    分页参数
```


#### DQL-基本查询
1.查询多个字段
```SQL
SELECT 字段1,字段2,字段3,... FROM 表名;
SELECT * FROM 表名
```

2.设置别名
```SQL
SELECT 字段1[AS 别名1],字段2[AS 别名2] ... FROM 表名; AS可以省略
```

3.去除重复记录
```SQL
SELECT DISTINCT 字段列表 FROM 表名;
```

#### DQL-条件查询
1.语法
```SQL
SELECT 字段列表 FROM 表名 WHERE 条件列表;
```
2.条件
| 比较运算符 | 功能 |                                 
|------------|-----|
|    >      | 大于 |
|>=         |大于等于|
|<          |小于   |
|<=         |小于等于|
| =         | 等于   |
|<> 或 !=   | 不等于 |
|BETWEEN...AND..|在某个范围之内(含最小，最大值)|
|IN(...)|在in之后的列表中的值，多选一(类似or的使用)|
|LIKE 占位符 |模糊匹配(_匹配单个字符，%匹配任意个字符)|
|IS NULL|是NULL|


|逻辑运算符|功能|
|----------|----|
|AND 或 && |并且(多个条件同时成立)|
|OR 或   | 或者 |
| NOT 或 ! | 非，不是|

* 例子
```SQL
# 查询姓名为两个字的员工信息
select * from emp where name like '__';

# 查询身份证最后一位是X的员工信息
select * from emp where id_card like '%X';
```


#### DQL-聚合函数
1.介绍
    将一列数据作为一个整体，进行纵向运算

2.常见聚合函数
|  函数  |  功能  |
|--------|-------|
|count|统计数量|
|max|最大值|
|min|最小值|
|avg|平均值|
|sum|求和|

3.语法
```SQL
SELECT 聚合函数(字段列表) FROM 表名;
```
* 所有的NULL值不参与聚合函数的运算



#### DQL-分组查询
1.语法
```SQL
SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件];
```
* where 和 having 区别
  * 执行时机不同:where是分组之前进行过滤，不满足where条件，不参与分组，而having是分组之后对结果进行过滤
  * 判断条件不同:where不能对聚合函数进行判断，而having可以
  
* 注意:
  * 执行顺序:where > 聚合函数 > having
  * 分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无意义


#### DQL-排序查询
1.语法
```SQL
SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1,字段2 排序方式2;
```
2.排序方式
* ASC:升序（默认值）
* DESC:降序
注意：如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序



#### DQL-分页查询
1.语法
```SQL
SELECT 字段列表 FROM 表名 LIMIT 起始索引,查询记录数;
```
注意
  * 起始索引从0开始，起始索引=（查询页码-1）* 每页显示记录数
  * 分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT
  * 如果查询的是第一页的数据，起始索引可以省略，直接简写为limit10



### DQL-执行顺序

```SQL
SELECT      4
    字段列表
FROM        1
    表名列表          
WHERE       2
    条件列表          
GROUP BY    3
    分组字段列表      
HAVING      
    分组后条件列表
ORDER BY    5
    排序字段列表
LIMIT       6
    分页参数
```