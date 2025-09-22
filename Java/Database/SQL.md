## 结构化查询语言
SQL(Structured Query Language)是一种用于管理和操作关系型数据库的标准化编程语言。
## DDL
**DDL(Data Definition Language)** 数据定义语言，用来对数据库中的数据对象的组成和结构进行定义。
### 操作数据库
- **查询数据库**
```mysql
-- 1.查询MySQL中所有的数据库
SHOW DATABASES;

-- 2.查询当前正在使用的数据库
SELECT DATABASE();
```
- **创建数据库**
```mysql
-- 1.普通创建（创建已经存在的数据库会报错）
CREATE DATABASE 数据库名称;

-- 2.创建并判断（该数据库不存在才创建）
CREATE DATABASE IF NOT EXISTS 数据库名称;

-- 创建一个数据库，并指定字符集
create DATABASE 数据库名称 DEFAULT charset utf8mb4;
```
- **删除数据库**
```mysql
-- 1.普通删除（删除不存在的数据库会报错） 
DROP DATABASE 数据库名称;

-- 2.删除并判断（该数据库存在才删除） 
DROP DATABASE IF EXISTS 数据库名称;
```
- **使用数据库**
```mysql
USE 数据库名称;
```
### 操作表
- **创建(CREATE)**
```mysql
CREATE TABLE 表名(
	字段名1 数据类型,
	字段名2 数据类型,
	...
	字段名n 数据类型  -- 最后一行不能加逗号！
);
```
- **查询(RETRIEVE，检索)**
```mysql
-- 1.查询当前数据库中所有表的名称
SHOW TABLES;

-- 2.查询表的结构
DESC 表名;

-- 3.查看建表语句（还能查看到建表时没写的默认参数）
show create table 表名;
```
- **修改(ALTER)**
```mysql
-- 1.修改表名
ALTER TABLE 表名 RENAME TO 新的表名;

-- 2.添加一列
ALTER TABLE 表名 ADD 列名 数据类型 [ COMMENT 注释 ];

-- 3.修改某列（字段）数据类型
ALTER TABLE 表名 MODIFY 列名 新的数据类型;

-- 4.修改列名和数据数据类型
ALTER TABLE 表名 CHANGE 旧列名 新列名 新数据类型 [ COMMENT 注释 ];

-- 5.删除列（字段）
ALTER TABLE 表名 DROP 列名;
```
- **删除(DROP)**
```mysql
-- 1.普通删除（删除不存在的表会报错）
DROP TABLE 表名;

-- 2.删除并判断（该表存在才删除）
DROP TABLE IF EXISTS 表名;

-- 3.删除指定表并重新创建（相当于清空表中的数据）
TRUNCATE TABLE 表名;
```
## DML
**DML(Data Manipulation Language)** 数据操作语言，用来对数据库库中表的数据进行增、删、改。
- **添加数据(INSERT)**
```mysql
-- 1.给指定列添加数据
INSERT INTO 表名(列名1,[列名2],[...) VALUES(值1,[值2],[...]); -- 值1对应列名1,...

-- 2.给全部列添加数据（相当于添加新的一行）
INSERT INTO 表名[所有列名] VALUES(值1,值2,...);
-- []中表示可以省略，省略时默认按顺序填写字段，不建议省略

-- 3.批量添加数据
INSERT INTO 表名(列名1,[列名2],[...]) VALUES(值1,值2,...),[(值1,值2,...)],[...];

-- 4.批量给全部列添加数据（相当于添加新的多行）
INSERT INTO 表名[所有列名] VALUES(值1,值2,...),(值1,值2,...),...;
```
- **修改数据(UPDATE)**
```mysql
UPDATE 表名 SET 列名1=值1,[列名2=值2],[...][WHERE 条件];
-- 注意：如果不使用WHERE条件，会将表中所有数据进行修改！
```
- **删除数据(DELETE)**
```mysql
DELETE FROM 表名 [WHERE 条件];
-- 注意：如果不使用WHERE条件，会将表中所有的数据删除！
```
## DQL
**DQL(Data Query Language)** 数据查询语言，用来查询数据库中表的数据。
### 基础关键字
- **查询所有记录**
```mysql
-- 查询users表中的所有记录
SELECT * FROM users;

-- 查询orders表中的所有记录
SELECT * FROM orders;
```
- **查询特定列**
```mysql
-- 查询users表中的name和email列
SELECT name, email FROM users;

-- 查询orders表中的user_id和amount列
SELECT user_id, amount FROM orders;
```
### 排序查询(order by)
- **按年龄排序**
```mysql
-- 按age列升序排序查询users表中的所有记录
SELECT * FROM users ORDER BY age ASC;

-- 按age列降序排序查询users表中的所有记录
SELECT * FROM users ORDER BY age DESC;

-- 按amount列升序排序查询orders表中的所有记录
SELECT * FROM orders ORDER BY amount ASC;
```
### 聚合函数
- **计算总数**
```mysql
-- 计算users表中的总记录数
SELECT COUNT(*) FROM users;

-- 计算orders表中的总记录数
SELECT COUNT(*) FROM orders;
```
- **计算平均值**
```mysql
-- 计算users表中age列的平均值
SELECT AVG(age) FROM users;

-- 计算orders表中amount列的平均值
SELECT AVG(amount) FROM orders;
```
- **计算总和**
```mysql
-- 计算orders表中amount列的总和
SELECT SUM(amount) FROM orders;
```
- **计算最大值和最小值**
```mysql
-- 计算users表中age列的最大值
SELECT MAX(age) FROM users;

-- 计算orders表中amount列的最小值
SELECT MIN(amount) FROM orders;
```
### 分组查询(group by)
- **按年龄分组**
```mysql
-- 按age分组并统计每组的人数
SELECT age, COUNT(*) FROM users GROUP BY age;

-- 按user_id分组并统计每组的总订单金额
SELECT user_id, SUM(amount) FROM orders GROUP BY user_id;
```
### 分页查询
- **分页查询**
```mysql
-- 查询users表中从第2页开始的10条记录（假设每页10条记录）
SELECT * FROM users LIMIT 10 OFFSET 10;

-- 查询orders表中从第3页开始的5条记录（假设每页5条记录）
SELECT * FROM orders LIMIT 5 OFFSET 10;
```
### 内连接查询
- **隐式内连接**
```mysql
-- 使用where条件消除无用数据，连接users和orders表
SELECT users.name, orders.amount 
FROM users, orders 
WHERE users.id = orders.user_id;

-- 查询所有用户及其订单信息
SELECT users.name, orders.amount 
FROM users, orders 
WHERE users.id = orders.user_id;
```
- **显式内连接**
```mysql
-- 使用INNER JOIN显式连接users和orders表
SELECT users.name, orders.amount 
FROM users 
INNER JOIN orders ON users.id = orders.user_id;

-- 查询所有用户及其订单信息
SELECT users.name, orders.amount 
FROM users 
INNER JOIN orders ON users.id = orders.user_id;
```
### 外连接查询
- **左外连接**
```mysql
-- 查询左表（users）所有数据以及其交集部分
SELECT users.name, orders.amount 
FROM users 
LEFT JOIN orders ON users.id = orders.user_id;

-- 查询所有用户及其订单信息，包括没有订单的用户
SELECT users.name, orders.amount 
FROM users 
LEFT JOIN orders ON users.id = orders.user_id;
```
- **右外连接**
```mysql
-- 查询右表（orders）所有数据以及其交集部分
SELECT users.name, orders.amount 
FROM users 
RIGHT JOIN orders ON users.id = orders.user_id;

-- 查询所有订单及其对应的用户信息，包括没有用户信息的订单
SELECT users.name, orders.amount 
FROM users 
RIGHT JOIN orders ON users.id = orders.user_id;
```
### 子查询
- **子查询的结果是单行单列的**
```mysql
-- 查询年龄最大的用户
SELECT * 
FROM users 
WHERE age = (SELECT MAX(age) FROM users);

-- 查询订单金额最大的订单的用户信息
SELECT * 
FROM users 
WHERE id = (SELECT user_id FROM orders WHERE amount = (SELECT MAX(amount) FROM orders));
```
- **子查询的结果是多行单列的**
```mysql
-- 查询所有年龄大于30岁的用户
SELECT * 
FROM users 
WHERE age > (SELECT age FROM users WHERE age = 30);

-- 查询所有有订单的用户信息
SELECT * 
FROM users 
WHERE id IN (SELECT user_id FROM orders);
```
## DCL
**DCL(Data Control Language)** 数据控制语言，用于权限管理
- **查询权限**
```mysql
-- 查询当前用户的权限
SHOW GRANTS FOR CURRENT_USER;

-- 查询名为'username'用户的权限
SHOW GRANTS FOR 'username'@'localhost';
```
- **授予权限**
```mysql
-- 授予'username'用户对test_db数据库的所有权限
GRANT ALL PRIVILEGES ON test_db.* TO 'username'@'localhost';

-- 授予'admin'用户对所有数据库的SELECT和INSERT权限
GRANT SELECT, INSERT ON *.* TO 'admin'@'localhost';
```
- **撤销权限**
```mysql
-- 撤销'username'用户对test_db数据库的所有权限
REVOKE ALL PRIVILEGES ON test_db.* FROM 'username'@'localhost';

-- 撤销'admin'用户对所有数据库的SELECT和INSERT权限
REVOKE SELECT, INSERT ON *.* FROM 'admin'@'localhost';
```