## 事务简介
* **事务** 是一组操作的集合，它是一个不可分割的工作单位，事务会把所有操作作为一个整体一起向系统提交或撤销操作请求，即这些操作 **要么同时成功，要么同时失败**

* 默认MySQL的事务是自动提交的，也就是说，当执行一条DML语句，MySQL会立即隐式的提交事务

## 事务操作

##### 转账案例 
```SQL
create table account(
    id int auto_increment primary key comment '主键ID',
    name varchar(10) comment '姓名',
    money int comment '金额'
) comment '账户表';

insert into account (id,name,money) values (null,'张三',2000),(null,'李四',2000);

-- 转账操作(张三给李四1000)
-- 1.查询张三账户
select * from account where name = '张三';
-- 2.将张三账户余额-1000
update account set money = money - 1000 where name = '张三';
程序抛出异常...
-- 3.将李四账户余额+1000
update account set money = money + 1000 where name = '李四';

```
* 在account表中，张三的钱减少了1000，但是李四的钱并没有增加1000


## 事务操作
##### 方式一
* 查看/设置事务提交方式，设置为手动提交
```SQL
SELECT @@autocommit;
SET @@autocommit = 0;
```

* 提交事务
```SQL
COMMIT;
```
* 回滚事务
```SQL
ROLLBACK;
```

###### 转账案例
```SQL
select @@autocommit;
set @@autocommit = 0; -- 设置手动提交

-- 转账操作(张三给李四1000)
-- 1.查询张三账户
select * from account where name = '张三';
-- 2.将张三账户余额-1000
update account set money = money - 1000 where name = '张三';
-- 程序抛出异常...
-- 3.将李四账户余额+1000
update account set money = money + 1000 where name = '李四';

-- 发生错误，回滚事务
rollback ;

-- 提交事务
commit;
```



##### 方式二
* 开启事务
```SQL
START TRANSACTION 或 BEGIN;
```

* 提交事务
```SQL
COMMIT;
```
* 回滚事务
```SQL
ROLLBACK;
```

***注意***: 选择了开启事务也表示手动控制事务，只要没有commit数据库中的数据就不会发生变化，事务执行失败则执行rollback


## 事务的四大特性(ACID)
1. **原子性(Atomicity) :** 事务是不可分割的最小操作单元，要么全部成功，要么全部失败。
2. **一致性(Consistency) :** 事务完成时，必须使所有的数据都保持一致状态
3. **隔离性(Isolation) :** 数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行
4. **持久性(Durability) :** 事务一旦提交或回滚，它对数据库中的数据的改变就是永久的


## 并发事务问题

* 并发事务问题指的是多个并发事务在执行的过程当中出现脏读、不可重复读、幻读的问题

|问题|描述|
|---|----|
|脏读|一个事务读到另外一个事务还没有提交的数据|
|不可重复读|一个事务先后读取同一条记录，但两次读取的数据不同，称之为不可重复读|
|幻读|一个事务按照条件查询数据时，没有对应的数据行，但是在插入数据时，又发现这行数据已经存在，好像出现了幻影|


## 事务隔离级别

|隔离级别|脏读|不可重复读|幻读|
|-------|----|----------|----|
|Read uncommitted|√|√|√|
|Read committed|x|√|√|
|Repeatable Read(默认)|x|x|√|
|Serializable|x|x|x|

```SQL
--查看事务隔离级别
SELECT@@TRANSACTION_ISOLATION;

--设置事务隔离级别
SET [SESSION|GLOBAL] TRANSACTION ISOLATION LEVEL {READ UNCOMMITTED | READ COMMITTED | REPEATABLE READ | SERIALIZABLE}

```

* 事务隔离级别越高，数据越安全，但是性能越低。


