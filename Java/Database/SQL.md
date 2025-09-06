## 结构化查询语言
SQL(Structured Query Language)是一种用于管理和操作关系型数据库的标准化编程语言。
## DDL
DDL(Data Definition Language 数据定义语言)用来对数据库中的数据对象的组成和结构进行定义。
### 操作数据库
- **查询数据库**
```sql
# 1.查询MySQL中所有的数据库
SHOW DATABASES;

# 2.查询当前正在使用的数据库
SELECT DATABASE();
```
- **创建数据库**
```sql
# 1.普通创建（创建已经存在的数据库会报错）
CREATE DATABASE my_database;

# 2.创建并判断（该数据库不存在才创建）
CREATE DATABASE IF NOT EXISTS my_database;

# 创建一个数据库，并指定字符集
create database my_database default charset utf8mb4;
```
- **删除数据库**
```sql
# 1.普通删除（删除不存在的数据库会报错） 
DROP DATABASE my_database;

# 2.删除并判断（该数据库存在才删除） 
DROP DATABASE IF EXISTS my_database;
```
- **使用数据库**
```sql

```
## DML

## DQL

## DCL