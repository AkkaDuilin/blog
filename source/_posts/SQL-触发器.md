---
title: SQL-触发器
categories:
  - 数据库

  - null
tags:
  - SQL
  - 数据库
copyright: true
date: 2022-05-16 21:33:46
permalink:
description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**


触发器与存储过程非常相似，触发器也是 SQL 语句集，它是通过事件进行触发而被执行的，不能用 EXECUTE 语句调用；而存储过程可以通过存储过程名字而被直接调用。当对某一表进行诸如 UPDATE、INSERT、DELETE 这些操作时，SQL Server 就会自动执行触发器所定义的 SQL 语句，从而确保对数据的处理必须符合由这些 SQL 语句所定义的规则。


<!-- more -->

# DML触发器

## 分类
1. AFTER 触发器
又称后触发器。在执行了 INSERT、UPDATE 或 DELETE 语句操作之后执行 AFTER 
触发器。如果仅指定 FOR 关键字，则 AFTER 为默认值。AFTER 触发器只能在表上指定，
可以为任何一个 DML 操作定义多个 AFTER 触发器

2. INSTEAD OF 触发器
又称替代触发器。INSTEAD OF 触发器在数据变动之前被触发，代替引起触发器执行
的 T-SQL 语句，即 INSTEAD OF 触发器执行时并不执行所定义的 INSERT、UPDATE 或
DELETE 操作，而仅执行触发器本身。

## 相关的逻辑表
Inserted 表用于存储 INSERT 和 UPDATE 语句所影响的行的副本。在插入或更新事务
期间，新行将同时被添加到 Inserted 表和触发器表（即对其尝试执行了用户操作的表）。
Inserted 表中的行是触发器表中的新行的副本。
Deleted 表用于存储 DELETE 和 UPDATE 语句所影响的行的副本。在执行 DELETE 
或 UPDATE 语句的过程中，行从触发器表中删除，并传输到 Deleted 表中。Deleted 表和触
发器表通常没有相同的行。

## 创建
{% codeblock  %}
CREATE TRIGGER trigger_name 
ON { OBJECT NAME } 
{ FOR → AFTER → INSTEAD OF } 
{[INSERT][,][UPFATE][,][DELETE]} 
 AS 
{ sql_statement [ ...n ] }
{% endcodeblock %}

1） trigger_name ：指定触发器名称
2） OBJECT NAME ：要对其执行 DML 触发器的表或视图
3） { FOR → AFTER → INSTEAD OF } ：指定触发器的类型，如果仅指定 FOR 关键
字，则 AFTER 是默认值
4） {[INSERT][,][UPDATE][,][DELETE]} ：指定激活触发器的数据修改语句，必须至少
指定一项，在触发器定义中允许使用上述选项的任意顺序组合。
5） sql_statement：指定触发器所指定的 T-SQL 语句。
6） 在 DML 触发器中不允许使用下列 Transact-SQL 语句：CREATE /ALTER/ DROP 
DATABASE、CREATE/DROP INDEX、DROP TABLE；用于执行以下操作的 ALTER TABLE：
添加、修改或删除列、添加或删除 PRIMARY KEY 或 UNIQUE 约束。

## 例题
创建一个触发器，在修改 SC 表中的 grade 列时，判断平均成绩是否大于 80，
如果大于 80，拒绝该修改操作。
{% codeblock  %}
CREATE TRIGGER trgUpdateSC ON dbo.SC
FOR UPDATE
AS
begin
  IF UPDATE (Grade)
    BEGIN
    --判断平均 grade 是否大于 80，如果大于 80，回滚
    if(select avg(Grade) from dbo.SC)>80
      begin
      print 'The average value of Grade cannot be more than 80'
      rollback
      end
  end
end
{% endcodeblock %}


# DDL触发器
DDL 触发器当服务器或者数据库中发生数据定义语言（DDL，CREATE、ALTER 和
DROP）事件时将被触发。

## 创建
{% codeblock  %}
CREATE TRIGGER trigger_name 
ON { ALL SERVER → DATABASE } 
[ WITH <ddl_trigger_option> [ ,...n ] ]
{ FOR → AFTER } { event_type → event_group } [ ,...n ]
AS { sql_statement [ ; ] [ ,...n ]}
{% endcodeblock %}

1） DATABASE :将 DDL 触发器的作用域应用于当前数据库。如果指定了此参数，则
只要当前数据库中出现 event_type 或 event_group，就会激发该触发器。
2） ALL SERVER :将 DDL 触发器的作用域应用于当前服务器。如果指定了此参数，
则只要当前服务器中的任何位置上出现 event_type 或 event_group，就会激发该触发器。
3） event_type ：执行之后将导致激发 DDL 触发器的 T-SQL 语言事件的名称。
4） event_group ：预定义的 T-SQL 语言事件分组的名称。执行任何属于 event_group 
的 T-SQL 语言事件之后，都将激发 DDL 触发器。

## 例题

为“Music”数据库创建 DDL 触发器，用于禁止对数据库中的表进行删除和修改操作。

{% codeblock  %}
CREATE TRIGGER trg_safe ON DATABASE 
FOR DROP_TABLE, ALTER_TABLE 
AS 
PRINT 'You must disable Trigger " trg_safe" to drop or alter tables!' 
ROLLBACK
{% endcodeblock %}

# 管理触发器

## 查看
{% codeblock  %}
exec sp_helptext trg_delete
{% endcodeblock %}
## 修改
{% codeblock  %}
ALTER TRIGGER trigger_name
ON { table → view }
{ { FOR → AFTER → INSTEAD OF }
{ [DELETE] [,] [INSERT] [,] [UPDATE] }
AS
{sql_statement}}
{% endcodeblock %}
## 删除
{% codeblock  %}
DROP TRIGGER Trg_delete
{% endcodeblock %}
## 禁用
{% codeblock  %}
1）禁用对表的 DML 触发器
DISABLE TRIGGER trg_delete ON Songs

2）禁用对数据库的 DDL 触发器
DISABLE TRIGGER trig_DDL ON DATABASE

3）禁用以同一作用域定义的所有触发器
DISABLE TRIGGER ALL ON ALL SERVER
{% endcodeblock %}

禁用之后的启用操作，应该使用语句 ENABLE TRIGGER，该语句的参数与对应的禁用语句相同。



<hr />
版权信息