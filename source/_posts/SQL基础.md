---
title: SQL基础
categories:
  - 数据库

  - null
tags:
  - SQL
  - 数据库
copyright: true
date: 2022-03-10 15:47:30
permalink:
description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**

**SQL学习笔记**

**持续更新ing**
https://www.runoob.com/sql/sql-tutorial.htmlhttps://www.runoob.com/sql/sql-tutorial.html
https://www.liaoxuefeng.com/wiki/1177760294764384


<!-- more -->

# 数据定义

## 数据库的定义

### 使用T-SQL创建
使用 SSMS 可以方便地创建数据库，但是，有些情况下不能使用图形化方式创建数据
库。比如在设计一个应用程序时，开发人员需要在程序代码中创建数据库及其他数据库对象，
而不用在制作应用程序安装包时再放置数据库或让用户自行创建，这就需要采用 T-SQL 语
句来创建数据库。

当使用 SSMS 向导创建数据库后，用户可以查看创建该数据库的 T-SQL 语句。方法是：
点击“对象资源管理器”→Music，点击右键快捷菜单中的“编写数据库脚本为”→“Create
到”→“新查询编辑器窗口”选项，在打开的查询编辑器窗口中，可以看到创建该数据库的
T-SQL 语句

**创建语句**
{% codeblock %}
CREATE DATABASE database_name /* 指定数据库逻辑文件名*/
[ON
  [PRIMARY]
  [<filespec> [1,…n]]
  [,<filegroup> [1,…n]]
]
/* ON 子句指定数据库的数据文件属性和文件组属性；其中 PRIMARY 指定关联的<filespec>列表定义主文件，如果没有定义 PRIMARY, 则 CREATE DATABASE语句中列出的第一个文件成为主文件 */

[LOG ON {<filespec> [1,…n]}] /* LOG ON 子句指定事务日志文件属性*/
{% endcodeblock %}


### 修改数据库
在 SQL Server 中，可用 ALTER DATABASE 语句修改数据库

其中< filespec >的格式同 CREATE DATABASE 中的< filespec >。

{% codeblock   %}
ALTER DATABASE database

ADD FILE < filespec > [ ,...n ]
/* 添加新的数据文件 */
[ TO FILEGROUP filegroup_name ]
/* 将要添加的数据文件添加到指
定的文件组中 */

ADD LOG FILE < filespec > [ ,...n ]
/* 添加新的事务日志文件 */
| REMOVE FILE logical_file_name
/* 删除某一文件 */

ADD FILEGROUP filegroup_name 
/* 添加一个文件组 */

REMOVE FILEGROUP filegroup_name
/* 删除一个文件组 */

MODIFY FILE < filespec > 
/* 修改某个文件的属性 */

MODIFY NAME = new_dbname 
/* 修改数据库的名字 */

MODIFY FILEGROUP filegroup_name {filegroup_property|NAME= new_filegroup_name }
/* 修改某个文件组的属性或为文件组定义一个新名字。文件组的属性有三种：READONLY（只读）、READWRITE（读写）、Default（默认） */

{% endcodeblock %}

### 删除数据库

使用 DROP DATABASE 语句删除数据库的语法如下：
{% codeblock   %}

DROP DATABASE database_name [,…n]

{% endcodeblock %}


### 例题
创建 Employee 数据库，要求如下：
1）主数据库文件名为 Employee，物理文件名为 Employee.mdf，初始大小为 5MB，最大文件大小为100MB，增长幅度为 1MB； 
2 ） 在 文 件 组 usergroup1 上 建 立 辅 助 数 据 文 件 Employee_dat ， 物 理 文 件 名 为
Employee_dat.ndf，初始大小为 3MB，最大为无限大，增幅为 1MB； 
3）日志文件逻辑文件名和物理文件名均为 Employee_log，初始大小为 3MB，最大为
20MB，增幅为 10%。以上文件均存储在为 E:\mssql2008\data 文件夹中。
4）为Employee数据库的usergroup2文件组添加一个辅助数据文件Employee_dat2，
要求：文件存储在 E:\mssql2008\data 文件夹下，初始大小为 10MB，最大为 20MB，增
幅为 5MB
5）删除 Employee 数据库的文件组 usergroup2
6）修改 Employee 中的数据文件 Employee_dat,将其初始大小改为 10MB，最大容
量改为 20MB，增幅设为 2MB。


{% codeblock %}
CREATE DATABASE Employee 
--定义主数据文件
ON PRIMARY 
( NAME =Employee, FILENAME = 'E:\mssql2008\data\Employee.mdf' , 
SIZE = 5, MAXSIZE = 100 , FILEGROWTH = 1KB ), 

--定义辅助数据文件
FILEGROUP usergroup1 
( NAME = Employee_dat, 
FILENAME = 'E:\mssql2008\data\Employee_dat.ndf' , 
SIZE = 3 , MAXSIZE = UNLIMITED, FILEGROWTH = 1)

--定义日志文件
LOG ON 
(NAME = Employee_log, 
FILENAME = 'E:\mssql2008\data\Employee_log.ldf' , 
SIZE = 3, MAXSIZE = 20, FILEGROWTH = 10%)

--添加数据文件
Alter DATABASE employee
Add file ( NAME = employee_dat2,
FILENAME='E:\mssql2008\data\Employee_dat2.mdf',
SIZE = 10, MAXSIZE = 50, FILEGROWTH = 5) to filegroup usergroup2

--删除文件组
--删除文件组中的文件
alter database employee remove file employee_dat2
--删除文件组
alter database employee remove filegroup usergroup2

--修改数据文件
AlTER DATABASE employee
MODIFY FILE
(NAME = Employee_dat, SIZE = 10, MAXSIZE = 20, FILEGROWTH = 2)

{% endcodeblock %}


## 基本表的定义

SQL Server 中，可以从两种角度来对表进行分类。
1. 按照数据存储的时间分类： 
1）永久表
表建立后，除非人工删除，否则一直保存。在 master、model、msdb 和用户数据库中建
立的表都是永久表。
2）临时表
临时表的数据只在数据库运行期间临时保存数据，临时表存储在 tempdb 中。

2. 按照表的用途来分类
1）用户表
用户创建的，用于开发各种数据库应用系统的表。
2）系统表
维护 SQL Server 服务器和数据库正常工作的数据表。每个数据库都会建立很多系统表，
这些表不允许用户进行更改，只能由 DBMS 自行维护。
3）临时表
SQL Server 的临时表有两种类型：本地临时表和全局临时表。
本地临时表只对于创建者是可见的。当用户与 SQL Server 实例断开连接后，将删除本
地临时表。
全局临时表在创建后对任何用户和任何连接都是可见的，当引用该表的所有用户都与
SQL Server 实例断开连接后，将删除全局临时表。
如果 SQL Server 服务器关闭，则所有的本地和全局临时表都被清空、关闭。
从表名称上来看，本地临时表的名称前面有一个“#”符号；而全局临时表的名称前面
有两个“##”符号 。
*说明：临时表的作用——当对数据库执行大数据量的排序等操作时，要产生大量的中间运算结果，因此需要消耗大量的内存资源。如果内存资源不够用，那么 SQL Server 将在临时数据库 tempdb中创建临时表用于存放这些中间结果。*
 4）分区表
当一个表中的数据量过于庞大时，可以使用分区表。分区表是将数据水平划分为多个单
元的表，这些单元可以分布到数据库中的多个文件组中。在维护整个集合的完整性时，使用
分区可以快速而有效地访问或管理数据子集，从而使大型表或索引更易于管理。

### 数据类型
|  序号 | 数据类型 | 含义 |
|:-----|:-----|:-----| 
|    1   |    char(n)    |  长度为n的定长字符串     |
|    2   |    varchar(n) |  最大程度为n的变长字符串 |
|    3   |     clob      |  字符串大对象            |
|    4   |     blob      |  二进制大对象            |
|    5   |     int       |  长整数(4 字节)          |
|    6   |     smallint  |  短整数(2 字节)          |
|    7   |     bigint    |  大整数(8 字节)          |
|    8   |     Numeric(10,2)    |  指字段是数字型,长度为10 小数为两位的 |          |
|    9   |     Date          |   YYYY-mm-dd     |
|    10   |     time          |    HH:ii:ss    |
|    11   |     Datetime          |   YYYY-mm-dd HH:ii:ss    |
|    12   |     Timestamp         |   时间戳类型 不为空 默认值为当前时间  |
|    13   |     float             |   浮点型，含字节数为4，32bit，数值范围为-3.4E38~3.4E38（7个有效位）|
|    14   |     double            |   双精度实型，含字节数为8，64bit数值范围-1.7E308~1.7E308（15个有效位）|
|    15   |     decimal           |   数字型，128bit，不存在精度损失，常用于银行帐目计算。（28个有效位）|

### 创建表
{% codeblock   %}

create table <表名> (
<列名><数据类型>[列级完整性约束条件]，
<列名><数据类型>[列级完整性约束条件]，
...
);

{% endcodeblock %}

eg：
<a href="https://sm.ms/image/ywXh2P7sROeGqfn" target="_blank"><img src="https://s2.loli.net/2022/03/10/ywXh2P7sROeGqfn.png" ></a>
{% codeblock   %}
CREATE TABLE Singer(
SingerID char(10) NOT NULL,
Name varchar(50) NOT NULL,
Gender varchar(2) NULL,
Birth datetime NULL,
Nation varchar(20) NULL
)
{% endcodeblock %}

### 列属性的设置

1. NULL
NULL（空值）表示数值未知或将在以后添加的数据。

2. DEFAULT
默认值是指当向表中插入数据时，如果用户没有明确给出某列的值，SQL Server 自动为
该列添加的值。

3. IDENTITY
使用 IDENTITY 关键字定义的字段又称标识字段。开发人员可以为标识字段指定标识
种子（Identity Seed 属性）和标识增量（Identity Increment 属性），系统按照给定的种子和增
量自动生成标识号，该标识号是唯一的。
使用 IDENTITY 属性时要注意：
一个表只能有一个使用 IDENTITY 属性定义的列; 
IDENTITY 只适用于 decimal（小数部分为 0）、int、numeric（小数部分为 0）、smallint、bigint 或 tinyint 数据类型；
标识种子和增量的默认值均为 1；  标识符列不能允许为空值，也不能包含 DEFAULT 定义或对象；
标识符列不能更新； 
如果在经常进行删除操作的表中存在标识符列，那么标识值之间可能会出现断缺。

{% codeblock   %}

create table Student
(
sno int not null identity(201102001,1), /*设置 IDENTITY*/
sname varchar(50) not null,
sex varchar(2),
hometown varchar(50) null default('江苏'), /*设置默认值*/
introuction varchar(50) null,
birthdate datetime not null )

{% endcodeblock %}


### 修改/删除表
表建立好后，一般不会再修改，但随着应用环境和需求的变化，偶尔也要修改已建立好
的表，SQL 语言用 ALTER TABLE 语句修改表，其一般格式为：
{% codeblock    %}
ALTER TABLE <表名>

[ ADD <新列名> <数据类型> <完整性约束>] /*增加新列*/

[DROP COLUMN <列名>] /*删除列*/

[ALTER COLUMN <列名> <数据类型>] /*修改列定义*/

[ADD <完整性约束>] /*添加约束*/

[DROP <完整性约束>] /*删除约束*/

// 当某个表不再需要时，可以使用 DROP TABLE 语句删除它。其一般格式为：

DROP TABLE <表名>
{% endcodeblock %}
其中<表名>是要修改的表，ADD 子句用于增加新列和新的完整性约束条件，DROP 子句用于删除指定的完整性约束条件，ALTER COLUMN 子句用于修改原有的列定义，包括修改列名和数据类型。


## 数据完整性的实现

{% post_link 数据库完整性 %}
{% post_link 数据库完整性 数据库完整性 %}


# 数据查询

{% post_link SQL数据查询 %}
{% post_link SQL数据查询 SQL数据查询 %}

# 数据更新

## 插入操作

元组插入语句的一般格式：
INSERT INTO <表名> ( <列名 1> [ , <列名 2>] …)
VALUES 
(<常量 1> [, <常量 2> ]…)
(<常量 11> [, <常量 22> ]…)
(<常量 111> [, <常量 222> ]…)
或者
INSERT INTO <表名> ( <列名 1> [ , <列名 2>] …)
<子查询>

{% codeblock    %}

假设另有一张歌手表 S，表结构与 Singer 一致，现在要求把 S 表中所有没有在
Singer 表里出现过的男歌星加入到 Singer 表中。

INSERT INTO Singers (SingerID, Name, Gender, Nation, Birth)
(
  SELECT (SingerID, Name, Gender, Nation, Birth)
  FROM S
  WHERE S.Gender=’男’ and NOT EXISTS (S.SingerID=Singers.SingerID)
)

{% endcodeblock %}

## 删除操作
SQL 删除语句的格式：

DELETE FROM <表名> ［WHERE <条件>］

如果没有 WHERE 子句，将会删除表中所有数据

{% codeblock    %}

删除歌手表中不是中国国籍的歌手
DELETE FROM Singers
WHERE Nation<>’中国’

{% endcodeblock %}

## 修改操作

当需要修改关系中元组的某些值时，可以用 UPDATE 语句实现。SQL 的 UPDATE 语句的
格式：

UPDATE <表名>
SET <列名>＝<值表达式>［，<列名>＝<值表达式>］… [WHERE <条件>］

如果省略 WHERE 子句，将会修改表中所有的元组

{% codeblock    %}

将 Singers 表中歌手编号为“GC002”的 Birth 属性值修改为 1978。

UPDATE Singers
SET Birth＝1978
WHERE SingerID＝' GC002

{% endcodeblock %}

# 索引与视图

## 索引 
建立索引以加快查询速度

1. 在表上创建一个简单的索引。允许使用重复的值：
{% codeblock   %}
CREATE INDEX index_name
ON table_name (column_name)
{% endcodeblock %}


2. 在表上创建一个唯一的索引。不允许使用重复的值：唯一的索引意味着两个行不能拥有相同的索引值
{% codeblock %}
CREATE UNIQUE INDEX index_name
ON table_name (column_name)
{% endcodeblock %}


3. 修改索引
{% codeblock %}
alter index index_name rename to new_name
{% endcodeblock %}


4. 删除索引
{% codeblock %}
drop index index_name
{% endcodeblock %}

## 视图 view
 
在 SQL 中，视图是基于 SQL 语句的结果集的可视化的表。
{% codeblock   %}
CREATE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition
{% endcodeblock %}

通过 DROP VIEW 命令来删除视图。
通过select 语句查询
通过update 语句更新 并不是所有视图都可以更新

<hr />
版权信息