## DCL介绍
### DCL是Data Control Language(数据控制语言),用来管理数据库用户、控制数据库的访问权限

#### DCL-管理用户

* 查询用户
```SQL
USE mysql;
SELECT * FROM user;
```

* 创建用户
```SQL
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码'
```

* 修改用户密码
```SQL
ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码'
```

* 删除用户
```SQL
DROP USER '用户名'@'主机名'
```

#### DCL-权限控制
* MySQL中定义了很多种权限，常用的有以下几种

|  权限  |   说明          |
|-------|------------------|
|ALL,ALL PRIVILEGES|所有权限|
|SELECT|查询数据|
|INSERT|插入数据|
|UPDATE|修改数据|
|DELETE|删除数据|
|ALTER|修改表|
|DROP|修改数据库/表/视图|
|CREATE|创建数据库/表|


* 查询权限
```SQL
SHOW GRANTS FOR '用户名'@'主机名';
```

* 授予权限
```SQL
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
```

* 撤销权限
```SQL
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
```
* 注意
  1.多个权限之间，使用逗号分隔
  2.授权时，数据库名和表名可以使用 * 进行通配，代表所有

