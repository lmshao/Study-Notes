## 1. 基本操作

连接数据库
```sh
$ mysql -u root -p
Enter password: ********
```

创建数据库
```sql
> create database dbname;
```

显示数据库
```sql
> show databases;
```

选择数据库
```sql
> use dbname;
```

查看数据表
```sql
> show tables;
```

查看数据表结构
```sql
> desc tbname;
```

删除数据表
```sql
> drop tbname;
```

删除数据库
```sql
> drop database dbname;
```

## 2. 数据类型

### 数值类型

类型|大小|范围（有符号）|范围（无符号）|用途
---|---|---|---|---
TINYINT|1 字节|(-128，127)|(0，255)|小整数值
SMALLINT|2 字节|(-32 768，32 767)| (0，65 535)|大整数值
INT或INTEGER|4 字节|(-2 147 483 648，2 147 483 647)|(0，4 294 967 295)|大整数值
BIGINT|8 字节|(-9 233 372 036 854 775 808，9 223 372 036 854 775 807)|(0，18 446 744 073 709 551 615)|极大整数值
FLOAT|4 字节|(-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38)|0，(1.175 494 351 E-38，3.402 823 466 E+38)|单精度浮点数值

### 日期类型
类型|大小(字节)|范围|格式|用途
---|---|---|---|---
DATE|3|1000-01-01/9999-12-31|YYYY-MM-DD|日期值
TIME|3|'-838:59:59'/'838:59:59'|HH:MM:SS|时间值或持续时间
YEAR|1|1901/2155|YYYY|年份值
DATETIME|8|1000-01-01 00:00:00/9999-12-31 23:59:59|	YYYY-MM-DD HH:MM:SS	|混合日期和时间值
TIMESTAMP|4|1970-01-01 00:00:00/2038|YYYYMMDD HHMMSS|混合日期和时间值，时间戳

### 字符串类型

类型|大小(字节)|用途
---|---|---
CHAR|0-255字节|定长字符串
VARCHAR|0-65535 字节|变长字符串
BLOB|0-65535字节|二进制形式数据，大小写敏感，可以保存图片二进制流
TEXT|0-65535字节|长文本数据，大小写不敏感
TINYBLOB|0-255字节|不超过 255 个字符的二进制字符串
TINYTEXT|0-255字节|短文本字符串
MEDIUMBLOB|0-16 777 215字节|二进制形式的中等长度文本数据
MEDIUMTEXT|0-16 777 215字节|中等长度文本数据
LONGBLOB|0-4 294 967 295字节|二进制形式的极大文本数据
LONGTEXT|0-4 294 967 295字节|极大文本数据

## 3. 创建数据表

语法
```sql
mysql> create table tab_name(col_name, col_type)
```

示例
```sql
mysql> create table if not exists report(
    ID INT UNSIGNED AUTO_INCREMENT,
    name VARCHAR(20) NOT NULL,
    math INT NOT NULL,
    music INT NOT NULL,
    art INT NOT NULL,
    PRIMARY KEY (ID)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
查看表结果
```sql
mysql> show tables;
+-------------------+
| Tables_in_student |
+-------------------+
| report            |
+-------------------+
1 row in set (0.00 sec)

mysql> desc report;
+-------+------------------+------+-----+---------+----------------+
| Field | Type             | Null | Key | Default | Extra          |
+-------+------------------+------+-----+---------+----------------+
| ID    | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| name  | varchar(20)      | NO   |     | NULL    |                |
| math  | int(11)          | NO   |     | NULL    |                |
| music | int(11)          | NO   |     | NULL    |                |
| art   | int(11)          | NO   |     | NULL    |                |
+-------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

```

## 4. 插入数据表

语法
```sql
mysql> insert into tab_name (field1, field2,...fieldN )
                            VALUES
                            (value1, value2,...valueN);
```

示例
```sql
mysql> insert into report
        (name, math, music, art) 
        VALUES 
        ("张三", 90, 91, 92);
mysql> insert into report
        (name, math, music, art)
        VALUES
        ("李四", 80, 81, 82);  
```

## 5. 查询数据

```sql
mysql> select col_name1, col_name2 from tbname;
        [WHERE Clause]
        [LIMIT N][OFFSET M]
```
- where 满足条件相应的条件，类似 if；
- limit: 指定记录条数；
- offset：记录偏移。
- 可以使用`*`表示显示全部列。
- BINARY关键字指定大小写。

示例：显示所有数据
```sql
mysql> select * from report;
+----+------+------+-------+-----+
| ID | name | math | music | art |
+----+------+------+-------+-----+
|  1 | Lucy |   90 |    91 |  92 |
|  2 | Mike |   80 |    81 |  82 |
|  3 | Lily |  100 |    99 |  98 |
+----+------+------+-------+-----+
3 rows in set (0.00 sec)
```

示例：显示指定条数和偏移
```sql
mysql> select ID, math, art from report LIMIT 2 OFFSET 1;
+----+------+-----+
| ID | math | art |
+----+------+-----+
|  2 |   80 |  82 |
|  3 |  100 |  98 |
+----+------+-----+
2 rows in set (0.00 sec)
```

示例：显示数学成绩大于90分的记录
```sql
mysql> select * from report where music > 90;
+----+------+------+-------+-----+
| ID | name | math | music | art |
+----+------+------+-------+-----+
|  1 | Lucy |   90 |    91 |  92 |
|  3 | Lily |  100 |    99 |  98 |
+----+------+------+-------+-----+
2 rows in set (0.00 sec)
```

示例：字符串大小写匹配，使用BINARY关键字指定大小写
```sql
mysql> select * from report where name="LuCY";
+----+------+------+-------+-----+
| ID | name | math | music | art |
+----+------+------+-------+-----+
|  1 | Lucy |   90 |    91 |  92 |
+----+------+------+-------+-----+
1 row in set (0.00 sec)

mysql> select * from report where BINARY name="LuCY";
Empty set (0.00 sec)
```

## 6. 更新数据
语法
```sql
> update tbname set field1=new-value1, field2=new-value2
[WHERE Clause]
```

示例：把Lucy的成绩都设为100分
```sql
mysql> update report set math=100, music=100, art=100 where name="Lucy";
Query OK, 1 row affected (0.22 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from report;
+----+------+------+-------+-----+
| ID | name | math | music | art |
+----+------+------+-------+-----+
|  1 | Lucy |  100 |   100 | 100 |
|  2 | Mike |   80 |    81 |  82 |
|  3 | Lily |  100 |    99 |  98 |
+----+------+------+-------+-----+
3 rows in set (0.00 sec)
```

## 6. 删除数据

语法
```sql
> delete from tbname [WHERE Clause]
```
不指定WHERE则删除所有记录。

示例：删除第二条记录
```sql
mysql> delete from report where id=2;
Query OK, 1 row affected (0.16 sec)

mysql> select * from report;
+----+------+------+-------+-----+
| ID | name | math | music | art |
+----+------+------+-------+-----+
|  1 | Lucy |  100 |   100 | 100 |
|  3 | Lily |  100 |    99 |  98 |
+----+------+------+-------+-----+
2 rows in set (0.00 sec)
```

## 模糊匹配 LIKE

类似于等号，使用`%`作为通配符
示例：查询名称带有L字母开头的记录

```sql
mysql> select * from report where name like 'L%';
+----+------+------+-------+-----+
| ID | name | math | music | art |
+----+------+------+-------+-----+
|  1 | Lucy |  100 |   100 | 100 |
|  3 | Lily |  100 |    99 |  98 |
+----+------+------+-------+-----+
2 rows in set (0.00 sec)
```

## 多条select选择 UNION

```sql
SELECT 列名称 FROM 表名称 UNION SELECT 列名称 FROM 表名称 ORDER BY 列名称;
SELECT 列名称 FROM 表名称 UNION ALL SELECT 列名称 FROM 表名称 ORDER BY 列名称;
```
UNION连接两条select语句，显示共有的元素，默认不重复显示，使用UNION ALL显示重复的所有元素。
示例：
有两个数据表info和report，
```sql
mysql> select * from info;
+----+------+------+-------------+
| ID | name | addr | tel         |
+----+------+------+-------------+
|  1 | Coco | USA  | 13012340001 |
|  2 | Dawn | CN   | 13012340002 |
|  3 | Ella | JP   | 13012340003 |
+----+------+------+-------------+
3 rows in set (0.01 sec)

mysql> select * from report;
+----+-------+------+-------+-----+
| ID | name  | math | music | art |
+----+-------+------+-------+-----+
|  1 | Lucy  |  100 |   100 | 100 |
|  3 | Lily  |  100 |    99 |  98 |
|  4 | Dawn  |   71 |    72 |  73 |
|  5 | Coco  |   61 |    62 |  63 |
|  6 | Adobe |   51 |    52 |  53 |
+----+-------+------+-------+-----+
5 rows in set (0.00 sec)

```

列出两个表中所有人的名字，不重复
```sql
mysql> select name from report
    -> union
    -> select name from info
    -> order by name;
+-------+
| name  |
+-------+
| Adobe |
| Coco  |
| Dawn  |
| Ella  |
| Lily  |
| Lucy  |
+-------+
6 rows in set (0.00 sec)
```

列出两个表中所有人的名字，重复
```sql
mysql> select name from report union all select name from info order by name;
+-------+
| name  |
+-------+
| Adobe |
| Coco  |
| Coco  |
| Dawn  |
| Dawn  |
| Ella  |
| Lily  |
| Lucy  |
+-------+
8 rows in set (0.00 sec)
```

### 排序

```sql
> order by
```

示例：对成绩单表按照art成绩排序，默认增序。
```sql
mysql> select * from report order by art;
+----+-------+------+-------+-----+
| ID | name  | math | music | art |
+----+-------+------+-------+-----+
|  6 | Adobe |   51 |    52 |  53 |
|  5 | Coco  |   61 |    62 |  63 |
|  4 | Dawn  |   71 |    72 |  73 |
|  3 | Lily  |  100 |    99 |  98 |
|  1 | Lucy  |  100 |   100 | 100 |
+----+-------+------+-------+-----+
5 rows in set (0.00 sec)
```

示例：降序排列，关键字DESC， 增序关键字ASC。
```sql
mysql> select * from report order by art DESC;
+----+-------+------+-------+-----+
| ID | name  | math | music | art |
+----+-------+------+-------+-----+
|  1 | Lucy  |  100 |   100 | 100 |
|  3 | Lily  |  100 |    99 |  98 |
|  4 | Dawn  |   71 |    72 |  73 |
|  5 | Coco  |   61 |    62 |  63 |
|  6 | Adobe |   51 |    52 |  53 |
+----+-------+------+-------+-----+
5 rows in set (0.00 sec)
```

### 条件判断中关于NULL的处理

应该使用`IS NULL`或者`IS NOT NULL`来进行判断，而不能使用等号。

### 正则表达式  

多条表达式中间使用`|`表示或。

```sql
> SELECT name FROM person_tbl WHERE name REGEXP '^st'; # 以st开头
> SELECT name FROM person_tbl WHERE name REGEXP 'ok$'; # 以ok结尾
> SELECT name FROM person_tbl WHERE name REGEXP 'mar'; # 包含mar字符串
> SELECT name FROM person_tbl WHERE name REGEXP '^[aeiou]|ok$'; # 以元音字符开头或者以ok结尾的字符串
```

## 导出数据库表

导出数据库
```sh
$ mysqldump -u root -p student > student.sql
```

还原数据库

```sh
$ mysql -uroot -p12345678 < student.sql
```

直接把数据库导出到远程主机数据库中

```sh
$ mysqldump -u root -p database_name \
       | mysql -h other-host.com database_name
```

远程数据库导出到本地
```sh
mysqldump -h other-host.com -P port -u root -p database_name > dump.txt
```