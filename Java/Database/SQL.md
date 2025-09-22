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
- **创建（CREATE）**
```mysql
CREATE TABLE 表名(
	字段名1 数据类型,
	字段名2 数据类型,
	...
	字段名n 数据类型  -- 最后一行不能加逗号！
);
```
- **查询（RETRIEVE，检索）**
```mysql
-- 1.查询当前数据库中所有表的名称
SHOW TABLES;

-- 2.查询表的结构
DESC 表名;

-- 3.查看建表语句（还能查看到建表时没写的默认参数）
show create table 表名;
```
- **修改（ALTER）**
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
- **删除（DROP）**
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
- **添加数据（INSERT）**
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
- **修改数据（UPDATE）**
```mysql
UPDATE 表名 SET 列名1=值1,[列名2=值2],[...][WHERE 条件];
-- 注意：如果不使用WHERE条件，会将表中所有数据进行修改！
```
- **删除数据（DELETE）**
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
### 排序查询（order by）
## DCL