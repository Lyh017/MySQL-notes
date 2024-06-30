# MySQL 笔记

## 概述
* 1.MySQL 启动
  net start mysql80
  net stop mysql80
* 2.MySQL 客户端连接
  mysql -u root -p

## SQL通用语法
* SQL语句可以单行或者多行书写，以分号结尾。
* SQL语句可以使用空格/缩进来增强语句的可读性。
* MySQL数据库的SQL语句不区分大小写，关键字建议用大写。
* 注释:
    * 单行注释：--注释内容 或# 注释内容(MySQL特有)
    * 多行注释：/*注释内容*/
  
## SQL分类
1.DDL Data Definition Language 数据定义语言，用来定义数据库对象（数据库，表，字段）
2.DML Data Manipulation Language 数据操作语言，用来对数据库表中的数据进行增删改
3.DQL Data Query Language 数据查询语言，用来查询数据库中的记录
4.DCL Data Control Language 数据控制语言，用来创建数据库用户，控制数据库的访问权限

### DDL-数据库操作
* 查询
  * 查询所有数据库
  ```SQL 
  SHOW DATABASES;
  ```
  * 查询当前数据库
  ```SQL
  SELECT DATABASE();
  ```
  * 创建数据库
  ```SQL
  CREATE DATABASE [IF NOT EXIST] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];
  ```
  * 删除数据库
  ```SQL
  DROP DATABASE [IF EXISTS] 数据库名;
  ```
  * 使用数据库
  ```SQL
  USE 数据库名;
  ```

#### DDL-表操作-查询 前提是通过use指令进入数据库

* 查询当前数据库所有表
  ```SQL
  SHOW TABLES;
  ```
* 查询表结构
  ```SQL
  DESC 表名;
  ```
* 查询指定表的建表语句
  ```SQL
  SHOW CREATE TABLE 表名;
  ```

#### DDL-表操作-创建
* 
```SQL
    CREATE TABLE 表名(
        字段1 字段1类型 comment,
        字段2 字段2类型 comment,
        ......
        字段n 字段n类型 comment
    ) comment表标注;
```
* 注意最后一个字段没有逗号

#### DDL-表操作-数据类型
* MySQL中的数据类型有很多，主要分为三类:数值类型，字符串类型，日期时间类型

#### DDL-表操作-修改
* DDL-表操作-修改
    * 添加字段
     ```SQL
    ALTER TABLE 表名 ADD 字段名 类型（长度）[COMMENT注释] 约束;
    ```
    * 修改数据类型
    ```SQL
    ALTER TABLE 表名 MODIFY 字段名 新数据类型（长度）;
    ```
    * 修改字段名和字段类型
    ```SQL
    ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型（长度） [COMMENT注释] 约束;
    ```
    * 删除字段
    ```SQL
    ALTER TABLE 表名 DROP 字段名;
    ```
    * 修改表名
    ```SQL
    ALTER TABLE 表名 RENAME TO 新表名;
    ```
    * 删除表，注意在删除表时，表中的数据也全部会被删除
    ```SQL
    DROP TABLE [IF EXISTS] 表名;
    ```
    * 删除指定表，并重新创建该表，只有表结构，没有数据
    ```SQL
    TRUNCATE TABLE 表名;
    ```





