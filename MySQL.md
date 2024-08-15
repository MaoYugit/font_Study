# 一. MySQL 连接

```bash
mysql -u root -p
```

```bash
[root@host] mysql -u root -p
Enter password:******
```

列出所有可用的数据库：

```bash
SHOW DATABASES;
```

选择要使用的数据库：

```bash
USE your_database;
```

列出所选数据库中的所有表：

```bash
SHOW TABLES;
```

退出 **mysql>** 命令提示窗口可以使用 **exit** 命令，如下所示：

```bash
mysql> EXIT;
Bye
```

或者使用：

```bash
mysql> QUIT;
```



# 二. MySQL 创建数据库

建数据库的基本语法如下：

```bash
CREATE DATABASE [IF NOT EXISTS] database_name
  [CHARACTER SET charset_name]
  [COLLATE collation_name];
```



# 三. MySQL 删除数据库

------

使用普通用户登陆 MySQL 服务器，你可能需要特定的权限来创建或者删除 MySQL 数据库，所以我们这边使用 root 用户登录，root 用户拥有最高权限。

在删除数据库过程中，务必要十分谨慎，因为在执行删除命令后，所有数据将会消失。



# 四. drop 命令删除数据库

drop 命令格式：

```bash
DROP DATABASE <database_name>;        -- 直接删除数据库，不检查是否存在
或
DROP DATABASE [IF EXISTS] <database_name>;
```



# 五. MySQL 选择数据库

在你连接到 MySQL 数据库后，可能有多个可以操作的数据库，所以你需要选择你要操作的数据库。

在 MySQL 中，要选择要使用的数据库，可以使用 **USE** 语句，以下是基本的语法：

```
USE database_name;
```



# 六. MySQL 数据类型

MySQL 中定义数据字段的类型对你数据库的优化是非常重要的。

MySQL 支持多种类型，大致可以分为三类：数值、日期/时间和字符串(字符)类型。

------

## 数值类型

MySQL 支持所有标准 SQL 数值数据类型。

这些类型包括严格数值数据类型(INTEGER、SMALLINT、DECIMAL 和 NUMERIC)，以及近似数值数据类型(FLOAT、REAL 和 DOUBLE PRECISION)。

关键字INT是INTEGER的同义词，关键字DEC是DECIMAL的同义词。

BIT数据类型保存位字段值，并且支持 MyISAM、MEMORY、InnoDB 和 BDB表。

作为 SQL 标准的扩展，MySQL 也支持整数类型 TINYINT、MEDIUMINT 和 BIGINT。下面的表显示了需要的每个整数类型的存储和范围。

| 类型         | 大小                                     | 范围（有符号）                                               | 范围（无符号）                                               | 用途            |
| :----------- | :--------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------- |
| TINYINT      | 1 Bytes                                  | (-128，127)                                                  | (0，255)                                                     | 小整数值        |
| SMALLINT     | 2 Bytes                                  | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值        |
| MEDIUMINT    | 3 Bytes                                  | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值        |
| INT或INTEGER | 4 Bytes                                  | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值        |
| BIGINT       | 8 Bytes                                  | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值      |
| FLOAT        | 4 Bytes                                  | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度 浮点数值 |
| DOUBLE       | 8 Bytes                                  | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度 浮点数值 |
| DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值          |

------

## 日期和时间类型

表示时间值的日期和时间类型为DATETIME、DATE、TIMESTAMP、TIME和YEAR。

每个时间类型有一个有效值范围和一个"零"值，当指定不合法的MySQL不能表示的值时使用"零"值。

TIMESTAMP类型有专有的自动更新特性，将在后面描述。

| 类型      | 大小 ( bytes) | 范围                                                         | 格式                | 用途                     |
| :-------- | :------------ | :----------------------------------------------------------- | :------------------ | :----------------------- |
| DATE      | 3             | 1000-01-01/9999-12-31                                        | YYYY-MM-DD          | 日期值                   |
| TIME      | 3             | '-838:59:59'/'838:59:59'                                     | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1             | 1901/2155                                                    | YYYY                | 年份值                   |
| DATETIME  | 8             | '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59'               | YYYY-MM-DD hh:mm:ss | 混合日期和时间值         |
| TIMESTAMP | 4             | '1970-01-01 00:00:01' UTC 到 '2038-01-19 03:14:07' UTC结束时间是第 **2147483647** 秒，北京时间 **2038-1-19 11:14:07**，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYY-MM-DD hh:mm:ss | 混合日期和时间值，时间戳 |

------

## 字符串类型

字符串类型指CHAR、VARCHAR、BINARY、VARBINARY、BLOB、TEXT、ENUM和SET。该节描述了这些类型如何工作以及如何在查询中使用这些类型。

| 类型       | 大小                  | 用途                            |
| :--------- | :-------------------- | :------------------------------ |
| CHAR       | 0-255 bytes           | 定长字符串                      |
| VARCHAR    | 0-65535 bytes         | 变长字符串                      |
| TINYBLOB   | 0-255 bytes           | 不超过 255 个字符的二进制字符串 |
| TINYTEXT   | 0-255 bytes           | 短文本字符串                    |
| BLOB       | 0-65 535 bytes        | 二进制形式的长文本数据          |
| TEXT       | 0-65 535 bytes        | 长文本数据                      |
| MEDIUMBLOB | 0-16 777 215 bytes    | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT | 0-16 777 215 bytes    | 中等长度文本数据                |
| LONGBLOB   | 0-4 294 967 295 bytes | 二进制形式的极大文本数据        |
| LONGTEXT   | 0-4 294 967 295 bytes | 极大文本数据                    |

**注意**：char(n) 和 varchar(n) 中括号中 n 代表字符的个数，并不代表字节个数，比如 CHAR(30) 就可以存储 30 个字符。

CHAR 和 VARCHAR 类型类似，但它们保存和检索的方式不同。它们的最大长度和是否尾部空格被保留等方面也不同。在存储或检索过程中不进行大小写转换。

BINARY 和 VARBINARY 类似于 CHAR 和 VARCHAR，不同的是它们包含二进制字符串而不要非二进制字符串。也就是说，它们包含字节字符串而不是字符字符串。这说明它们没有字符集，并且排序和比较基于列值字节的数值值。

BLOB 是一个二进制大对象，可以容纳可变数量的数据。有 4 种 BLOB 类型：TINYBLOB、BLOB、MEDIUMBLOB 和 LONGBLOB。它们区别在于可容纳存储范围不同。

有 4 种 TEXT 类型：TINYTEXT、TEXT、MEDIUMTEXT 和 LONGTEXT。对应的这 4 种 BLOB 类型，可存储的最大长度不同，可根据实际情况选择。

------

## 枚举与集合类型（Enumeration and Set Types）

- **ENUM**: 枚举类型，用于存储单一值，可以选择一个预定义的集合。
- **SET**: 集合类型，用于存储多个值，可以选择多个预定义的集合。

------

## 空间数据类型（Spatial Data Types）

GEOMETRY, POINT, LINESTRING, POLYGON, MULTIPOINT, MULTILINESTRING, MULTIPOLYGON, GEOMETRYCOLLECTION: 用于存储空间数据（地理信息、几何图形等）。



# 七. MySQL 创建数据表

创建 MySQL 数据表需要以下信息：

- 表名
- 表字段名
- 定义每个表字段的数据类型

### 语法

以下为创建 MySQL 数据表的 SQL 通用语法：

```
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```

**参数说明：**

- `table_name` 是你要创建的表的名称。
- `column1`, `column2`, ... 是表中的列名。
- `datatype` 是每个列的数据类型。

以下是一个具体的实例，创建一个用户表 **users**：

### 实例1

**CREATE** **TABLE** users (
  id **INT** **AUTO_INCREMENT** **PRIMARY** **KEY**,
  username **VARCHAR**(50) **NOT** **NULL**,
  email **VARCHAR**(100) **NOT** **NULL**,
  birthdate **DATE**,
  is_active **BOOLEAN** **DEFAULT** **TRUE**
);

实例解析：

- `id`: 用户 id，整数类型，自增长，作为主键。
- `username`: 用户名，变长字符串，不允许为空。
- `email`: 用户邮箱，变长字符串，不允许为空。
- `birthdate`: 用户的生日，日期类型。
- `is_active`: 用户是否已经激活，布尔类型，默认值为 true。

以上只是一个简单的实例，用到了一些常见的数据类型包括 INT, VARCHAR, DATE, BOOLEAN，你可以根据实际需要选择不同的数据类型。AUTO_INCREMENT 关键字用于创建一个自增长的列，PRIMARY KEY 用于定义主键。

如果你希望在创建表时指定数据引擎，字符集和排序规则等，可以使用 **CHARACTER SET** 和 **COLLATE** 子句：

### 实例2

**CREATE** **TABLE** mytable (
  id **INT** **PRIMARY** **KEY**,
  name **VARCHAR**(50)
) **CHARACTER** **SET** utf8mb4 **COLLATE** utf8mb4_general_ci;

以上代码创建一个使用 utf8mb4 字符集和 utf8mb4_general_ci 排序规则的表。

以下例子中我们将在 RUNOOB 数据库中创建数据表 runoob_tbl：

### 实例3

**CREATE** **TABLE** **IF** **NOT** **EXISTS** `runoob_tbl`(
  `runoob_id` **INT** **UNSIGNED** **AUTO_INCREMENT**,
  `runoob_title` **VARCHAR**(100) **NOT** **NULL**,
  `runoob_author` **VARCHAR**(40) **NOT** **NULL**,
  `submission_date` **DATE**,
  **PRIMARY** **KEY** ( `runoob_id` )
)ENGINE=InnoDB **DEFAULT** CHARSET=utf8;

实例解析：

- 如果你不想字段为**空**可以设置字段的属性为 **NOT NULL**，如上实例中的 runoob_title 与 runoob_author 字段， 在操作数据库时如果输入该字段的数据为空，就会报错。
- **AUTO_INCREMENT** 定义列为自增的属性，一般用于主键，数值会自动加 1。
- **PRIMARY KEY** 关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号 **,** 分隔。
- **ENGINE** 设置存储引擎，**CHARSET** 设置编码。



# 八. MySQL 删除数据表

MySQL中删除数据表是非常容易操作的，但是你在进行删除表操作时要非常小心，因为执行删除命令后所有数据都会消失。

### 语法

以下为删除 MySQL 数据表的通用语法：

```bash
DROP TABLE table_name ;    -- 直接删除表，不检查是否存在
或
DROP TABLE [IF EXISTS] table_name;
```





# 九. MySQL 插入数据

MySQL 表中使用 **INSERT INTO** 语句来插入数据。

你可以通过 **mysql>** 命令提示窗口中向数据表中插入数据，或者通过PHP脚本来插入数据。

### 语法

以下为向MySQL数据表插入数据通用的 **INSERT INTO** SQL语法：

```
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

**参数说明：**

- `table_name` 是你要插入数据的表的名称。
- `column1`, `column2`, `column3`, ... 是表中的列名。
- `value1`, `value2`, `value3`, ... 是要插入的具体数值。

如果数据是字符型，必须使用单引号 **'** 或者双引号 **"**，如： 'value1', "value1"。

一个简单的实例，插入了一行数据到名为 users 的表中：

```
INSERT INTO users (username, email, birthdate, is_active)
VALUES ('test', 'test@runoob.com', '1990-01-01', true);
```

- `username`: 用户名，字符串类型。
- `email`: 邮箱地址，字符串类型。
- `birthdate`: 用户生日， 日期类型。
- `is_active`: 是否已激活，布尔类型。

如果你要插入所有列的数据，可以省略列名：

```
INSERT INTO users
VALUES (NULL,'test', 'test@runoob.com', '1990-01-01', true);
```

这里，**NULL** 是用于自增长列的占位符，表示系统将为 **id** 列生成一个唯一的值。

如果你要插入多行数据，可以在 VALUES 子句中指定多组数值：

```
INSERT INTO users (username, email, birthdate, is_active)
VALUES
    ('test1', 'test1@runoob.com', '1985-07-10', true),
    ('test2', 'test2@runoob.com', '1988-11-25', false),
    ('test3', 'test3@runoob.com', '1993-05-03', true);
```

以上代码将在 users 表中插入三行数据。



# 十. MySQL 查询数据

MySQL 数据库使用 **SELECT** 语句来查询数据。

你可以通过 **mysql>** 命令提示窗口中在数据库中查询数据，或者通过 PHP 脚本来查询数据。

### 语法

以下为在 MySQL 数据库中查询数据通用的 SELECT 语法：

```
SELECT column1, column2, ...
FROM table_name
[WHERE condition]
[ORDER BY column_name [ASC | DESC]]
[LIMIT number];
```

**参数说明：**

- `column1`, `column2`, ... 是你想要选择的列的名称，如果使用 `*` 表示选择所有列。
- `table_name` 是你要从中查询数据的表的名称。
- `WHERE condition` 是一个可选的子句，用于指定过滤条件，只返回符合条件的行。
- `ORDER BY column_name [ASC | DESC]` 是一个可选的子句，用于指定结果集的排序顺序，默认是升序（ASC）。
- `LIMIT number` 是一个可选的子句，用于限制返回的行数。

MySQL SELECT 语句简单的应用实例：

### 实例1

*-- 选择所有列的所有行*
**SELECT** * **FROM** users;

*-- 选择特定列的所有行*
**SELECT** username, email **FROM** users;

*-- 添加 WHERE 子句，选择满足条件的行*
**SELECT** * **FROM** users **WHERE** is_active = **TRUE**;

*-- 添加 ORDER BY 子句，按照某列的升序排序*
**SELECT** * **FROM** users **ORDER** **BY** birthdate;

*-- 添加 ORDER BY 子句，按照某列的降序排序*
**SELECT** * **FROM** users **ORDER** **BY** birthdate **DESC**;

*-- 添加 LIMIT 子句，限制返回的行数*
**SELECT** * **FROM** users **LIMIT** 10;

SELECT 语句可以是灵活的，我们可以根据实际需求组合和使用这些子句，比如同时使用 WHERE 和 ORDER BY 子句，或者使用 LIMIT 控制返回的行数。

在 `WHERE` 子句中，你可以使用各种条件运算符（如 `=`, `<`, `>`, `<=`, `>=`, `!=`），逻辑运算符（如 `AND`, `OR`, `NOT`），以及通配符（如 `%`）等。

以下是一些进阶的 SELECT 语句实例：

### 实例2

*-- 使用 AND 运算符和通配符*
**SELECT** * **FROM** users **WHERE** username **LIKE** 'j%' **AND** is_active = **TRUE**;

*-- 使用 OR 运算符*
**SELECT** * **FROM** users **WHERE** is_active = **TRUE** **OR** birthdate < '1990-01-01';

*-- 使用 IN 子句*
**SELECT** * **FROM** users **WHERE** birthdate **IN** ('1990-01-01', '1992-03-15', '1993-05-03');