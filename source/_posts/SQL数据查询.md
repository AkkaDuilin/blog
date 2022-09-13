---
title: SQL数据查询
categories:
  - 数据库

  - null
tags:
  - SQL
  - 数据库
  - 关系代数
copyright: true
date: 2022-03-23 09:59:50
permalink:

description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**

SQL的查询相关代码

https://blog.csdn.net/weixin_44176696/article/details/112586831

<!-- more -->


# SQL语句

## 基本结构

数据查询是数据库的核心操作，SQL 使用 SELECT 语句进行数据库的查询，其一般格式
为：

{% codeblock    %}
SELECT [ ALL｜DISTINCT ] < 目标列表达式 > [，<目标列表达式 > …] 
FROM < 表名或视图名 > [，<表名或视图名>… ] 
[ WHERE < 条件表达式> ]
[ GROUP BY < 列名列表> [ HAVING < 条件表达式> ] ]
[ ORDER BY < 列名> [ ASC ｜DESC ] ]；
{% endcodeblock %}

（1） []：表示[]中的内容是可选的，比如[ WHERE < 条件表达式> ]，表示可以使用 WHERE 也可以不使用

（2） <>：表示<>中的内容必须出现。比如< 表名或视图名 >，这个部分表示从哪个地方获取数据，是不可或缺的。

（3） ｜：表示选择其一，例如 < 列名 2> [ ASC ｜DESC ] ]，表示列名 2 后只能用ASC或者DESC其中之一来进行结果的排序，前者代表升序，后者代表降序。

（4） [，…]：表示括号中的内容可以重复出现 1 至多次。

（5） * 表示相应范围内的所有内容 select * 表示查找表中所有数据

## 列操作

### 查询列
在 SQL 语句中，用 FROM 子句指定要操纵的表，SELECT 子句给出要投影的列，对应的 SQL 语句如下：
{% codeblock    %}
select A,B 
from T_A

select * 
from T_B
{% endcodeblock %}
SELECT 语句的执行结果是一个新表，这个表没有名字，是个临时表，它的关系模式由SELECT 子句里的属性列构成

select * 表示查找全部列

### 列别名
有时候，我们希望查询结果中的某些列名不同于基本表中的列名，这时，可以在 SELECT
子句中增加列别名。
SQL 语句使用 AS 关键词对列设置“别名”。AS 使用格式如下：

旧名 AS 别名

eg：
查询曲库里的所有歌曲的详细信息，请把表中的各个列名：SongID，Name，Lyricist，Composer，Lang 分别替换成：歌曲编号、歌曲名称、词作者、曲作者、语言类别。
{% codeblock    %}
SELECT SongID AS 歌曲编号, Name AS 歌曲名称, Lyricist AS 词作者,Composer AS 曲作者, Lang AS 语言类别
FROM Songs;
{% endcodeblock %}

### 查询计算列
SELECT 子句的<目标列表达式>不仅可以是表中真实存在的列，也可以是一个表达式。可以使用常量计算表达式或者函数。
{% codeblock    %}
SELECT SongID, SingerID, Circulation*10000 as NewCirculation
FROM Track

SELECT Name as 姓名, Birth as 出生日期, 2012-Year（Birth） as 年龄
FROM Singers
{% endcodeblock %}

### 过滤重复列
两条本来并不完全相同的元组，投影到某些列上后，可能变成相同的行了，可以用DISTINCT 关键字过滤它们。
{% codeblock    %}
SELECT DISTINCT Style
FROM Track;
{% endcodeblock %}


## where 子句

WHERE 子句用于表达关系代数中选择运算的选择条件。
<a href="https://sm.ms/image/dJUMtu5DN2VwaYr" target="_blank"><img src="https://s2.loli.net/2022/03/24/dJUMtu5DN2VwaYr.png" ></a>

逻辑运算符 AND 和 OR 可以用来联结多个查询条件。**AND 的优先级高于 OR**，但用户可以用括号来改变优先级。

### 确定范围

比较运算符包括：=（等于），>（大于），<(小于)，>=（大于等于），<=（小于等于），!=
或者<>（不等于）。

谓词 BETWEEN…AND 用于查询列值在指定范围内]的元组，其中 BETWEEN 后面跟的
是范围下限，AND 后跟的是范围的上限。

{% codeblock    %}
SELECT Name, Birth
FROM Singers
Where Birth<1967

求查询出生年份不在 1970~1980 之间的歌手的姓名与性别
SELECT Name, Gender
FROM Singers
WHERE Birth NOT BETWEEN 1970 AND 1980;
{% endcodeblock %}


### 字段匹配
谓词 LIKE 可以用来进行字符串的匹配。 其一般语法格式如下：

列名 [NOT] LIKE ‘<匹配串>’ [ESCAPE ‘<换码字符>’]


其含义是查找列值与<匹配串>相匹配的元组。通常，<匹配串>中可以使用通配符“%”（百分号）和“_”（下横线）。
其中：
%：代表任意长度（长度可以为 0）的字符串。例如，a%b 表示以 a 开头、以 b 结尾的
任意长度的字符串。字符串 ab、axb、agxb 都满足该匹配串。
_：代表任意单个字符。例如，a_b 表示以 a 开头，以 b 结尾，中间夹一个字符的任意字
符串。如 axb、a!b 等都满足要求。

如果用户要查询的字符串本身就含有%或_，这时就要使用’ESCAPE<换码字符>’对通配
符进行转义

{% codeblock    %}
查询歌手编号以“GC”开头的歌手姓名、性别。
SELECT Name, Gender
FROM Singers
WHERE SingerID like ‘GC%’

查询以”John_”开头的歌手的详细信息。
SELECT *
FROM Singers
WHERE Name like ‘John\_%’ ESCAPE ’\’;
{% endcodeblock %}


### 确定集合/判空
谓词 IN 用来查找某个列值属于指定集合的元组，格式为：

列名 IN/NOTT IN 集合 (x , x , x , x )

谓词 IS NULL 用于判断某列的值是否为空值，格式如下：

列名 IS NULL

{% codeblock    %}
查询曲目表中既不属于“乡村”、“爵士”也不是“摇滚”曲风的专辑详细信息。
SELECT SongID, SingerID
FROM Track
WHERE Style NOT IN (‘乡村’, ‘爵士’ , ‘摇滚’);

查询曲目表中缺少发行量信息的记录。
SELECT *
FROM Track
WHERE Circulation IS NULL;

{% endcodeblock %}


## order by 子句
由 SELECT-FROM-WHERE 构成的 SELECT 查询语句完成对表的选择和投影操作，得到一个新的结果表，还可以对得到的新表做进一步的操作。

ORDER BY 子句用于对查询结果进行排序。**可以按照一个或者多个属性列进行升序（ASC）或者降序(DESC)排列**，默认将按照升序排列。

{% codeblock    %}
查询曲目表中的歌手编号、歌曲编号和曲风类别，将查询结果按照发行时间降序排列。

SELECT SongID, SingerID, Style
FROM Track
ORDER BY PubYear DESC,SingerID ASC;

{% endcodeblock %}


## 聚集函数

AVG()：返回某列的平均值

COUNT()：返回某列的行数

MAX()：返回某列的最大值

MIN()：返回某列的最小值

SUM()：返回某列值之和
如果指定 DISTINCT 标识符，则表示计算时要取消指定列中的重复值。如果不指定DISTINCT 或指定 ALL（ALL 为缺省），则表示不取消重复值。

{% codeblock    %}
查询 Track 表中的记录总数，最早发行时间、最近发行时间和整个发行量的总和。

SELECT Count(*) as 记录总数, MIN(PubYear) as ‘最早发行量’, MAX(PubYear) as ‘最近发行
时间’, SUM(Circulation) as ‘发行量总和’

FROM Track
{% endcodeblock %}

## group by 子句
聚合函数是对查询结果（一个元组集）中的值进行统计。在有的查询中，我们要把具有相同特征的元组分成若干子集，然后需要再对每个子集中的值进行统计，此时就要用到SELECT 句型中的分组子句“GROUP BY”，格式为:

GROUP BY <列名列表>
{% codeblock    %}
mysql> SELECT * FROM access_log;
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
|   6 |       4 |    13 | 2016-05-15 |
|   7 |       3 |   220 | 2016-05-15 |
|   8 |       5 |   545 | 2016-05-16 |
|   9 |       3 |   201 | 2016-05-17 |
+-----+---------+-------+------------+
9 rows in set (0.00 sec)

统计 access_log 各个 site_id 的访问量：
SELECT site_id, SUM(access_log.count) AS nums
FROM access_log GROUP BY site_id;
{% endcodeblock %}

在用分组语句时，SELECT 后跟的列只能是聚集函数或者是出现在 GROUP BY 之后的分组列。

## having 子句
在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与聚合函数一起使用。

HAVING 子句可以让我们筛选分组后的各组数据。

https://www.runoob.com/sql/sql-having.html

{% codeblock    %}
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value;
{% endcodeblock %}


## 笛卡儿积和连接

SQL 在一个查询中建立几个表的联系的方法非常简单，只要在 FROM 子句中列出所有
涉及到的表就可以了。从概念上讲，FROM 子句先对这些表做笛卡尔积操作，得到一个临
时表，以后的选择、投影等操作都是针对这个临时表，从而将多表查询转换为单表查询。

一般格式为

**[<表名 1>.]<列名 1> <比较运算符> [<表名 2>.]<列名 2>**

## join 子句

<a href="https://sm.ms/image/KJqzfrO1AQtiM9u" target="_blank"><img src="https://s2.loli.net/2022/03/30/KJqzfrO1AQtiM9u.jpg" ></a>

### 内连接

在非 ANSI 标准的实现中，连接是在 WHERE 子句中执行的（即在 WHERE 子句中指定表间的连接条件）；在 ANSI SQL-92 中，连接是在 JOIN 子句中执行的。前者称为Theta 连接，后者称为 ANSI 连接。

ANSI 内连接的语法格式：
FROM 表 1 [INNER] JOIN 表 2 ON <连接条件>

{% codeblock    %}

eg ：列出曲库中所有演唱过歌曲的歌手名，歌曲名和发行量。

Theta 方式的 SQL 语句：
SELECT Songs.Name AS 歌曲名, Singers.Name AS 歌手名,Circulation AS 发行量
FROM Songs,Track,Singers
WHERE Songs.SongID=Track.SongID AND Track.SingerID=Singers.SingerID


ANSI 方式的 SQL 语句为：
SELECT Songs.Name AS 歌曲名, Singers.Name AS 歌手名,Circulation AS 发行量
FROM Songs JOIN Track ON Songs.SongID=Track.SongID
JOIN Singers ON Track.SingerID=Singers.SingerID

{% endcodeblock %}

### 自身连接

**连接操作不仅可以在两个表之间进行，也可以与其自身进行连接，称为表的自身连接。**

可以为表提供别名，其格式如下：
FROM <源表名> [AS] <表别名>

{% codeblock    %}

SELECT FIRST.CNumber， SECOND.PCNumber
FROM Course FIRST， Course SECOND
WHERE FIRST.PCNumber=SECOND.CNumber；

{% endcodeblock %}

### 外连接

外连接之限制一张表中的数据必须满足连接条件，而另一张表中的数据可以不满足连接
条件。

Theta 方式的外连接语法格式为：
左外连接：FROM 表 1，表 2 WHERE [表 1.]列名(+)=[表 2.]列名
右外连接：FROM 表 1，表 2 WHERE [表 1.]列名=[表 2.]列名(+)

ANSI 方式的外连接语法格式为：
FROM 表 1 LEFT | RIGHT JOIN [OUTER] 表 2 ON <连接条件>

SQL SERVER 支持 ANSI 方式的外连接，但 ORACLE 支持的是 Theta 方式的外连接。

{% codeblock    %}

SELECT column_name(s)
FROM table1
FULL OUTER/RIGHT/LEFT JOIN table2
ON table1.column_name=table2.column_name;

    
{% endcodeblock %}

## 子查询

在实际应用中，经常有一些 SELECT 语句需要使用其他 SELECT 语句的查询结果，此时就需要用到子查询。

### IN谓词子查询

其格式如下：
SELECT <列名> [,<列名>] …
FROM <表名>
WHERE <表达式> <[NOT] IN | 其它比较运算符>
( 
  SELECT <列名> 
  FROM <表名> 
  WHERE <条件> 
）

NOT IN 执行的是集合运算 其他运算符执行比较运算

使用 IN 运算时，如果表达式的值与集合中的某个值相等，则此运算结果为真；如果表达式的值与集合中的所有值均不相等，则运算结果为假。由关键字 IN 引入的子查询的 SELECT 后的列名只允许有 1 项内容，即只能是一个列名或者是表达式。

使用子查询进行比较运算时，通过比较运算符（=、<>、<、>、<=、>=），将一个表达式的值与子查询返回的值进行比较。如果比较运算的结果为真，则比较运算返回 TRUE。使用子查询进行比较测试时，要求子查询语句必须是返回单值的查询语句。

{% codeblock    %}

查询歌唱风格是“摇滚”的歌手信息。

SELECT *
FROM Singers
WHERE SingerID IN
(
  SELECT DISTINCT SingerID
  FROM Track
  WHERE Style =’摇滚’ 
)

{% endcodeblock %}

### 带有比较运算符的子查询

使用子查询进行比较运算时，通过比较运算符（=、<>、<、>、<=、>=），将一个表达式的值与子查询返回的值进行比较。如果比较运算的结果为真，则比较运算返回 TRUE。使用子查询进行比较测试时，要求子查询语句必须是返回单值的查询语句。

{% codeblock    %}
查询年龄最大的歌手的信息

SELECT *
FROM Singers
WHERE Birth =
(
  SELECT MAX(Birth)
  FROM Singers
)

{% endcodeblock %}

### 带有ANY或ALL谓词的子查询

<a href="https://sm.ms/image/UVIQPu9qDElgR6o" target="_blank"><img src="https://s2.loli.net/2022/03/30/UVIQPu9qDElgR6o.jpg" ></a>

https://blog.csdn.net/qq_38157534/article/details/108527994

{% codeblock    %}

【例】查询非计算机科学系中比计算机科学系任意一个学生年龄小的学生姓名和年龄
select Sname，Sage 
from student
where Sage < ANY
  ( select  Sage 
    from student 
    where Sdept  = "CS") 
AND Sdept <> "CS";

{% endcodeblock    %}


### 带有EXISTS谓词的子查询

相关子查询通常使用 EXISTS 谓词，其形式为：
SELECT <列名> [,<列名>] …
FROM <表名>
WHERE
WHERE [NOT] EXISTS
( 
  SELECT * 
  FROM <表名> 
  WHERE <条件> 
)

带有 EXISTS 谓词的子查询不返回任何数据，只产生逻辑真值“true”或逻辑假值“false”：
*若内层查询结果非空，则外层的 WHERE 子句返回真值*
*若内层查询结果为空，则外层的 WHERE 子句返回假值*

{% codeblock    %}
查询歌唱风格是“摇滚”的歌手信息。

SELECT *
FROM Singers X
WHERE EXISTS
(
SELECT *
FROM Track
WHERE Track.SingerID=X.SingerID and Style =’摇滚’ )
{% endcodeblock %}

## 集合查询

SELECT 查询操作的对象是集合，结果也是集合。集合操作主要包括并操作 UNION，交操作 INTERSECT 和差操作 EXCEPT。

注意： 参加集合操作的各查询结果的列数必须相同；对应项的数据类型也要相同。

{% codeblock    %}
查询中国歌手和出生日期晚于 1960 年的歌手。

SELECT *
FROM Singers
WHERE Nation=’中国’
UNION
SELECT *
FROM Singers
WHERE Birth>=1960
{% endcodeblock %}

# xx3x

<hr />
版权信息