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

## DB-API

DB-API 是 Python 中访问关系型数据库的标准 API。使用它可以处理多种类型的关系型数据库，不需为每种类型编写独立的程序，类似于 Java 的 JDBC 或 Perl 的 dbi。

它的主要函数有：

- `connect()` 连接数据库，参数包含用户名、密码、服务器地址等等。
- `cursor()` 创建一个 cursor 对象来管理查询
- `execute()` 和 `executemany()` 对数据库执行一个或多个 SQL 命令
- `fetchone()` `fetchmany()` `fetchall()` 得到 execute 之后的结果

## SQLite

[SQLite][sqlite] 是一种轻量级的、优秀的开源关系型数据库。数据存储在普通文件中。

SQLite 仅仅支持原生 SQL 以及多用户并发操作。

首先使用 `connect()` 函数连接本地的 SQLite 数据库文件。字符串 `:memory:` 仅用于在内存中创建数据库，便于快速测试，但程序结束时所有数据会丢失。

下面创建一个数据库 `enterprise.db` 和表单 `zoo`。表单的列如下所示：

- `critter`: 可变长度字符串，主键。（critter: 生物）
- `count`: 动物总数，整数
- `damages`: 损失的美元数目。

```py
>>> import sqlite3
>>> conn = sqlite3.connect('enterprise.db')
>>> curs = conn.cursor()
>>> curs.execute('''CREATE TABLE zoo
... (critter VARCHAR(20) PRIMARY KEY,
... count INT,
... damages FLOAT)''')
<sqlite3.Cursor object at 0x10f50d730>
```

现在向动物园中新增一些动物：

```py
>>> curs.execute('INSERT INTO zoo VALUES("duck", 5, 0.0)')
<sqlite3.Cursor object at 0x10f50d730>
>>> curs.execute('INSERT INTO zoo VALUES("bear", 2, 1000.0)')
<sqlite3.Cursor object at 0x10f50d730>
```

使用 placeholader 是一种更安全的插入数据的方法：

```py
>>> ins = 'INSERT INTO zoo (critter, count, damages) VALUES(?, ?, ?)'
>>> curs.execute(ins, ('weasel', 1, 2000.0))
<sqlite3.Cursor object at 0x10f50d730>
```

在 SQL 中使用三个问号表示要插入三个值，并把它们作为一个列表传入函数 `execute()`。这些占位符用来处理一些冗余的细节，例如引号（quoting）。它们会防止 SQL 注入。

现在使用 SQL 获取所有的动物：

```py
>>> curs.execute('SELECT * FROM zoo')
<sqlite3.Cursor object at 0x10f50d730>
>>> rows = curs.fetchall()
>>> print(rows)
[('duck', 5, 0.0), ('bear', 2, 1000.0), ('weasel', 1, 2000.0)]
```

按照数目（count）排序，重新获得它们：

```py
>>> curs.execute('SELECT * FROM zoo ORDER BY count')
<sqlite3.Cursor object at 0x10f50d730>
>>> curs.fetchall()
[('weasel', 1, 2000.0), ('bear', 2, 1000.0), ('duck', 5, 0.0)]
```

又需要按照降序得到它们：

```py
>>> curs.execute('SELECT * FROM zoo ORDER BY count DESC')
<sqlite3.Cursor object at 0x10f50d730>
>>> curs.fetchall()
[('duck', 5, 0.0), ('bear', 2, 1000.0), ('weasel', 1, 2000.0)]
```

查找花费最多的动物：

```py
>>> curs.execute('''SELECT * FROM zoo WHERE damages = (SELECT MAX(damages) FROM zoo)''')
<sqlite3.Cursor object at 0x10f50d730>
>>> curs.fetchall()
[('weasel', 1, 2000.0)]
```

如果已经打开了一个连接或游标，不需要时应该关掉它们：

```py
>>> curs.close()
>>> conn.close()
```

## MySQL

（未完待续。。。）

## PostgreSQL

（未完待续。。。）

## SQLAlchemy

DB-API 仅仅实现不同关系型数据库共有的部分。

每种数据库实现的是包含自己特征和哲学的方言，许多库函数用于消除它们之间的差异，最著名的跨数据库 Python 库是 [SQLAlchemy][sqlalchemy]。

它不在 Python 的标准库中，安装方法如下：

```sh
pip install sqlachemy
```

可以在以下层级使用 SQLAlchemy：

- 底层负责处理数据库连接池、执行 SQL 命令以及返回结果，这和 DB-API 相似
- 再往上是 SQL **表达式语言**，更像 Python 的 SQL 生成器
- 较高级的是对象关系模型（ORM），使用 SQL 表达式语言，将应用程序代码和关系型数据结构结合起来。

使用 SQLAlchemy 时，不需要导入驱动程序，初始化的字符串会做出分配，例如：

```sh
dialect + driver :// user : password @ host : port / dbname
# dialect 数据库类型
# driver 使用该数据库的特定驱动程序
# user, password 数据库认证字符串
# host, port 数据库服务器的位置
# dbname 初始连接到服务器中的数据库
```

以下是常见方言和对应的驱动程序

| 方言 | 驱动程序 |
| --- | --- |
| sqlite | pysqlite（可忽略） |
| mysql | mysqlconnector |
| mysql | pymysql |
| mysql | oursql |
| postgresql | psycopg2 |
| postgresql | pypostgresql |

### 1. 引擎层

SQLAlchemey 底层可以实现多于基本 DB-API 的功能。

以内置于 Python 的 SQLite 为例，连接字符串忽略 host, port, user 和 password。dbname 表示存储 SQLite 数据库的文件。

如果省去 dbname，SQLite 会在内存创建数据库。

以下是一个例子：

```py
>>> import sqlalchemy as sa

>>> conn = sa.create_engine('sqlite://')
>>> conn.execute('''CREATE Table zoo
... (critter VARCHAR(20) PRIMARY KEY,
... count INT,
... damages FLOAT)''')
<sqlalchemy.engine.result.ResultProxy object at 0x1108c47f0>

>>> ins = 'INSERT INTO zoo (critter, count, damages) VALUES (?, ?, ?)'
>>> conn.execute(ins, 'duck', 10, 0.0)
<sqlalchemy.engine.result.ResultProxy object at 0x1108c4b00>
>>> conn.execute(ins, 'bear', 2, 1000.0)
<sqlalchemy.engine.result.ResultProxy object at 0x1108c4ba8>
>>> conn.execute(ins, 'weasel', 1, 2000.0)
<sqlalchemy.engine.result.ResultProxy object at 0x1108c4a20>

>>> rows = conn.execute('SELECT * FROM zoo')

# rows 不是一个列表，不能直接输出
>>> print(rows)
<sqlalchemy.engine.result.ResultProxy object at 0x1108c40f0>

# 可以像列表一样迭代，每次得到其中一行
>>> for row in rows:
...     print(row)
...
('duck', 10, 0.0)
('bear', 2, 1000.0)
('weasel', 1, 2000.0)
```

## REF
- [《Python语言及其应用》][douban] - 8.4 关系型数据库，*Bill Lubanovic*，人民邮电出版社，2016年1月出版

[douban]: https://book.douban.com/subject/26675127/
[sqlite]: http://www.sqlite.org
[sqlalchemy]: https://www.sqlalchemy.org