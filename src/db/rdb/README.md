# 关系型数据库

## SQL

SQL 是一种声明式语言，是关系型数据库的通用语言。

SQL 查询是客户端发送给数据库服务器的文本字符串，指明需要执行的具体操作。

SQL 语句主要有两种主要的类型：

- DDL（数据定义语言）：处理用户、数据库以及表单的创建、删除、约束和权限等。
- DML（数据操作语言）：处理数据插入、选择、更新和删除。

**基本的 SQL DDL 命令**

| 操作 | SQL 模式 | SQL 示例 |
| --- | --- | --- |
| 创建数据库 | CREATE DATABASE dbname | CREATE DATABASE d |
| 选择当前数据库 | USE dbname | USE d |
| 删除数据库以及表单 | DROP DATABASE dbname | DROP DATABASE d |
| 创建表单 | CREATE TABLE tbname(col defs) | CREATE TABLE t(id INT, count INT) |
| 删除表单 | DROP TABLE tbname | DROP TABLE t |
| 删除表单中所有的行 | TRUNCATE TABLE tbname | TRUNCATE TABLE t |

> SQL 是不区分大小写的，但是一般为了区分命令和名称，在代码示例中还是用大写字母。

SQL 关系型数据库的主要 DML 操作可以缩略为 CRUD：

- Create: 使用 INSERT 语句创建
- Read: 使用 SELECT 语句选择
- Update: 使用 UPDATE 语句更新
- Delete: 使用 DELETE 语句删除

**基本的 SQL DML 命令如下**

| 操作 | SQL 模式 | SQL 示例 |
| --- | --- | --- |
| 增加行 | INSERT INTO tbname VALUES(...) | INSERT INTO t VALUE(7, 40) |
| 选择全部行列 | SELECT * FROM tbname | SELECT * FROM t |
| 选择全部行和部分列 | SELECT cols FROM tbname | SELECT id, count FROM t |
| 选择部分行部分列 | SELECT cols FROM tbname WHERE condition | SELECT id,count FROM t WHERE count > 5 AND id = 9 |
| 修改一列的部分行 | UPDATE tbname SET col = value WHERE condition | UPDATE t SET count=3 WHERE id=5 |
| 删除部分行 | DELETE FROM tbname WHERE condition | DELETE FROM t WHERE count <= 10 OR id = 16 |