---
title: Transact-SQL
categories:
  - 数据库

  - null
tags:
  - SQL
  - 数据库
copyright: true
date: 2022-05-13 18:52:21
permalink:
description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**


SQL Server 在支持标准 SQL 语言的同时，对其进行了扩充，引入了 T-SQL，即 Transact-SQL。通过 T-SQL，可以定义变量、使用流控制语句、自定义函数和存储过程，极大地扩展了 SQL Server 的功能。


<!-- more -->

# 语法约定
<a href="https://sm.ms/image/ul2WgxJFGmYLaAs" target="_blank"><img src="https://s2.loli.net/2022/05/13/ul2WgxJFGmYLaAs.png" ></a>

## 注释 
注释语句不是可执行语句，不参与程序的编译、注释语句通常是用来说明代码的功能或
者对代码的实现方式给出简单的解释和提示。
在 T-SQL 中可使用两类注释符：
1. “--”用于单行注释；
2. “/* */”用于多行注释。“/*”用于注释文字的开头，“*/”用于注释文字的结束。


# 标识符
SQL Server 有两类标识符：
1）常规标识符：符合标识符的格式规则。在 T-SQL 语句中使用常规标识符时不用将其
分隔开。
**常规标识符的定义规则如下：**
  1） 名称的长度可以从 1 到 128（对于本地临时表，标识符最多可以有 116 个字符）。
  2） 名称的第一个字符必须是一个字母或者“_”、“@”和“#”中的任意字符。
  3） 在中文版 SQL Server 中，可以直接使用中文名称。
  4） 名称中不能有空格
  5） 不允许使用 SQL Server 的保留字。
2）分隔标识符：在 T-SQL 中，不符合常规标识符定义规则的标识符必须用分隔符双引
号 (") 或者方括号 ([ ])分隔，称为分隔标识符。例如：Select * from [my table]中，因为“my 
table”中间含有空格，不符合常规标识符的定义规则，因此必须用分隔符 ([ ])进行分隔。

**使用**
[[[server.][database].][owner_name].] object_name
1）server：本地服务器；
2）database：当前数据库；
3）owner_name：在数据库中与当前连接会话登录标识相关联的数据库用户名或数据库
所有者（dbo）。
例如，需要引用 customer 数据库中 employee 表的 telephone 列，可指定 customer.. 
employee.telephone。

# 常量
1. 字符串
单引号内

2. Unicode字符串
与普通字符串类似，前面有N标识

3. 二进制常量
前有 0x 标识

4. datetime 常量
datetime 常量使用特定格式的字符日期值来表示，并被单引号括起来。
下面是 datetime 常量的示例：
'December 5, 1985'； '5 December, 1985'； '12/5/98'
'851205'（其中的 0 不能省略）
下面是时间常量的示例：'14:30:24'； '04:24 PM'

5. int
不包含小数

6. decimal 
包含小数点的数字

7. float/real
科学计数法表示

8. money 
money 常量以前缀为可选的小数点和可选的货币符号的数字字符串来表示。money 常
量不使用引号括起。money 常量的示例：$542023.14，￥30。

# 变量

声明变量：
DECLARE @变量名 变量类型[,@变量名 变量类型…]

赋值：
SET @变量名=表达式
或：SELECT @局部变量=变量值

{% codeblock   %}
DECLARE @no varchar(10) 
--变量赋值
SET @no='Bj10001' 
--显示指定学生学号、姓名 
SELECT Sid,Sname FROM student WHERE SID=@no
{% endcodeblock %}

全局变量是 SQL Server 系统内部使用的变量，其作用范围并不局限于某一程序，而是
任何程序均可随时调用。
格式：@@变量名。
<a href="https://sm.ms/image/muU79kRgsFht4bn" target="_blank"><img src="https://s2.loli.net/2022/05/13/muU79kRgsFht4bn.png" alt="image.png"></a>

# 函数
1. ASCII 函数
 函数格式：
ASCII（character_expression）
功能：求 character_expression（char 或 varchar 类型）左端第一个字符的 ASCII 码。
返回值数据类型：int。例如：
Select ASCII（’abcd’） --结果为字符 a 的 ASCII 码 97。

2. CHAR 函数
 函数格式：
CHAR（integer_expression）
功能：求 ASCII 码 integer_expression 对应的字符，
integer_expression 的有效范围为[0,255]，如果超出范围，则返
回值 NULL。
返回值数据类型：CHAR。例如：
Select CHAR（97） --结果为'a'。 
CHAR 可用于将控制字符插入字符串中。表 9- 8 显示了
一些常用的控制字符。
例9- 6: 使用回车符。
select '**'+char(13)+'***'
结果如图 9- 1 所示（注意，显示该结果时，在查询编辑器中，
需在查询工具栏选择“以文本格式显示结果”）。

3. UNICODE 函数
语法:
UNICODE ( 'ncharacter_expression' )
功能：按照 Unicode 标准的定义，返回输入表达式的第一个字
符的整数值。
返回类型：int。例如：
Select unicode(N’kerge’) --返回字符 k 的 unicode 值 107

4. NCHAR 函数
语法：NCHAR ( integer_expression ) 
功能: 根据 Unicode 标准所进行的定义，用给定整数代码返回 Unicode 字符。
integer_expression 介于 0 与 65535 之间的所有正整数。如果指定了超出此范围的值，将返
回 NULL。
返回类型：nchar(1)。例如：
select nchar(107) --返回 unicode 字符 k

5. CHARINDEX 函数
函数格式：
CHARINDEX（expression1, expression2[,start]）
功能：在 expression2 中由 start 指定的位置开始查找 expression1 第一次出现的位置，如
表 9- 8 控制字符及值
控制字符 值
制表符 CHAR(9)
换行符 CHAR(10)
回车 CHAR(13)
图 9- 1 char 函数示例
果没有找到，则返回 0。如果省略 start，或 start≤0，则从 expression2 的第一个字符开始。
返回类型：int。例如：
Select CHARINDEX('ab', '123abc123abc') --结果为 4。

6. LEFT 函数
 函数格式：
LEFT（expression1,n）
功能：返回字符串 expression1 从左边开始 n 个字符组成的字符串。如果 n=0，则返回一
个空字符串。
返回类型：varchar。例如：
LEFT('abcde', 3) --结果为'abc'。 例 9- 7：找出 dbo.student 中名字以'刘'开头的学生信息。
select sno,sname from dbo.student where left(sname,1)='刘'

7. RIGHT 函数
函数格式：
RIGHT（expression1,n）
功能：返回字符串 expression1 从右边开始 n 个字符组成的字符串。如果 n=0，则返回一
个空字符串。
返回类型：varchar。例如：
Select RIGHT('abcde', 3) --结果为'cde'。

8. SUBSTRING 函数
函数格式：
SUBSTRING（expression1,start,length）
 功能：返回 expression1（数据类型为字符串、binary、text 或 image）中从 start 开始长
度为 length 个字符或字节的子串。
返回值：数据类型与 expression1 数据类型相同，但 text 类型返回值为 varchar，image 类
型返回值为 varbinary，next 类型返回值为 nvarchar。例如：
Select SUBSTRING('abcde123',3,4) --结果为'cde1'。 例 9- 7 也可以写成：
select sno,sname from dbo.student where substring(sname,1,1)='刘'

9. LEN 函数
函数格式：
LEN（expression1）
功能：返回字符串 expression1 中的字符个数，不包括字符串末尾的空格。
返回类型：int。例如：
Select LEN('abcde ') --结果为 5。
select len('刘') --结果为 1。

10. DATALENGTH 函数
DATALENGTH ( expression ) 
功能：返回用于表示任何表达式的字节数。
返回类型：int。例如：
Select DATALENGTH('abcde ') --结果为 8（含 3 个空格）。
select DATALENGTH('刘') --结果为 2。

11. LOWER 函数
 函数格式：
LOWER（expression1）
功能：将字符串 expression1 中的大写字母替换为小写字母。
返回类型：varchar。例如：
Select LOWER('12ABC45*%^def') --结果为'12abc45*%^def'。

12. UPPER 函数
 函数格式：
UPPER（expression1）
 功能：将字符串 expression1 中的小写字母替换为大写字母。
 返回类型：varchar。例如：
Select UPPER(‘12ABC45*%^def’) --结果为'12ABC45 *%^DEF'。

13. LTRIM 函数
函数格式：
LTRIM（expression1）
功能：删除字符串 expression1 左端的空格。
返回类型：varchar。例如：
Select LTRIM(' 12AB') --结果为'12AB'。

14. RTRIM 函数
函数格式：
RTRIM（expression1）
功能：删除字符串 expression1 末尾的空格。
返回类型：varchar。例如：
Select RTRIM(LTRIM(' 12AB ')) --结果为'12AB'。

15. REPLACE 函数
 函数格式：
REPLACE（expression1, expression2, expression3）
 功能：将字符串 expression1 中所有的子字符串 expression2 替换为 expression3。
 返回值数据类型：varchar。例如：
Select REPLACE('abcde','de','12') --结果为'abc12'。

16. STUFF 函数
语法:
STUFF (character_expression,start,length,character_expression ) 
功能：删除指定长度的字符并在指定的起始点插入另一组字符。
返回类型:如果 character_expression 是一个支持的字符数据类型，则返回字符数据。
例如：
Select STUFF('abcde',4,2,'12') --结果为'abc12'。

17. REVERSE 函数
 函数格式：
REVERSE（expression1）
 功能：按相反顺序返回字符串 expression1 中的字符。
 返回值数据类型：varchar。例如：
Select REVERSE ('edcba') --结果为 abcde。

18. SPACE 函数
 函数格式：
SPACE（n）
 功能：返回包含 n 个空格的字符串，如果 n 为负数，则返回一个空字符串。
 返回值数据类型：char。

19. STR 函数
 函数格式：
STR（expression1[,length[,decimal]]）
 功能：将数字数据转换为字符数据。length 为转换得到的字符串总长度，包括符号、小
数点、数字或空格。如果数字长度不够，则在左端加入空格补足长度，如果小数部分超过总
长度，则进行四舍五入，length 的默认值为 10，decimal 为小数位位数。
 返回值数据类型：char。例如：
 select str(123,6) --结果为' 123'
 select str(123.456,5) --结果为' 123'
 select str(123.456,5,2) --结果为'123.5'
 select str(123.456,8,2) --结果为' 123.46'

20. REPLICATE(character_expression,times)
语法：
REPLICATE(character_expression,times)
功能：返回多次复制后的字符表达式。times 参数的计算结果必须为整数。例如：
select replicate('*',3) --返回‘***’ 例 9- 8：以“*”方式输出菱形。
输出结果见 图 9- 2（在查询编辑器中以文本格式显示结果）。
declare @i int
set @i=1
while @i<=4
begin
print space(4-@i)+
replicate('*',2*@i-1)
set @i=@i+1
end
set @i=1
while @i<=3
begin
print space(@i)+replicate('*',7-2*@i)
set @i=@i+1
end

21. CAST 函数
功能：将一种数据类型的表达式转换为另一种数据类型的表达式。
语法：
CAST ( expression AS data_type [ (length ) ])
例：
--将日期时间类型转换为 char 类型
select cast('2010-3-2' as char(10))

22. CONVERT 函数
CONVERT 函数将一种数据类型的表达式转换为另一种数据类型的表达式。
语法：
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )

23. ISDATE 函数
语法：
ISDATE( expression )
功能：如果 expression 是 datetime 或 smalldatetime 数据类型的有效日期或时间值，则
返回 1；否则，返回 0。例如：
select ISDATE('2009/2/29') --返回 0

24. ISNULL ( check_expression , replacement_value )
语法：
ISNULL ( check_expression , replacement_value )
功能：如果 check_expression 不为 NULL，则返回它的值；否则，在将 replacement_value 
隐式转换为 check_expression 的类型（如果这两个类型不同）后，则返回前者。例如：
--如果成绩为 NULL，替换为 0
select grade as 成绩,ISNULL(grade,0) as ISNULL_结果 from sc

25. NULLIF 函数
NULLIF ( expression , expression )
功能：如果两个指定的表达式相等，则返回空值。

26. ISNUMERIC 函数
语法：
ISNUMERIC ( expression )
功能：确定表达式是否为有效的数值类型。

## 日期
1. GETDATE 函数
函数格式： 
图 9- 2 输出菱形
GETDATE（）
 功能：按 SQL Server 内部标准格式返回系统日期和时间。
 返回值数据类型：datetime。例如：
Select getdate() --结果为 2012-08-13 21:51:32.390
2. YEAR 函数
 函数格式：
YEAR（date）
功能：返回指定日期 date 中年的整数。
返回值数据类型：int。例如：
Select year('2004-3-5') --结果为 2004
例 9- 9：返回学生表中学生的年龄。
select sname as 学号, BirthDate as 出生日期,
YEAR(getdate())-YEAR(birthdate) as 年龄
from dbo.student
结果见图 9- 3 所示。
3. MONTH 函数
 函数格式：
MONTH（date）
 功能：返回指定日期 date 中月份的整数。
 返回值数据类型：int。例如：
Select month('2004-3-5') --结果为 3
4. DAY 函数
 函数格式：
DAY（date）
 功能：返回指定日期 date 中天的整数。
 返回值数据类型：int。例如：
Select day('2004-3-5') --结果为 5
5. DATENAME 函数
 函数格式：
 DATENAME（datepart,date）
功能：返回日期 date 中由 datepart 指定的日期部分的字符串。
返回类型：nvarchar。
6. DATEPART 函数
 函数格式：
 DATEPART（dateprrt,date）
 功能：与 DATENAME 类似，只是返回值为整数。
 返回值数据类型：int。
7. DATEADD 函数
 函数格式： 
DATEADD（dateprrt,n,date）
 功能：在 date 指定日期时间的 datepart 部分加上 n，得到一个新的日期时间值。
 返回值数据类型：datetime，如果参数 date 为 smalldatetime，则返回值为 smalldatetime
类型。参数 datepart 可以使用如表 9- 9 所示中的短语或缩写。例如：
Select dateadd(yy,2,'2012-3-4') --结果为’2014-03-04 00:00:00.000'
Select dateadd(m,2,'2012-3-4') --结果为'2012-05-04 00:00:00.000'
Select dateadd(d,2,'2012-3-4') --结果为'2012-03-06 00:00:00.000'
8. DATEDIFF 函数
格式：
DATEDIFF ( datepart , startdate , enddate )
功能：返回指定的 startdate 和 enddate 之间所跨的指定 datepart 边界的计数（带符号
的整数）。
例 9- 9：返回学生表中学生的年龄。
select sname as 学号, BirthDate as 出生日期,
DATEDIFF(yy, birthdate,getdate()) as 年龄 from dbo.student

datepart可选参数
日期部分 缩写 日期部分 缩写
年份 yy、yyyy 工作日 dw
季度 qq、q 小时 hh 
月份 mm、m 分钟 mi、n 
每年的某一日 dy、y 秒 ss、s 
图 9- 3 YEAR 函数示例
日期 dd、d 毫秒 ms 
星期 wk、ww 工作日 dw

# 批处理和流程控制语句

##  IF…ELSE 语句
1. 如果满足条件，则在 IF 关键字及其条件之后执行
T-SQL 语句。可选的 ELSE 关键字引入另一个 T-SQL 语句，当不满足 IF 条件时就执行该
语句。
2. 在实际程序中，IF…ELSE 语句中不止包含一条语句，而是一组的 SQL 语句。为了可以
一次执行一组 SQL 语句，这时就需要使用 BEGIN…END 语句将多条语句封闭起来。

eg 查找学号为 200215121 的成绩。
{% codeblock   %}
DECLARE @message varchar(255),@grade_num int
--得到 200215121 号同学的选修课程的数目
SELECT @grade_num=COUNT(grade) FROM sc 
WHERE sno='200215121'
IF @grade_num=0
 BEGIN
  SET @message= '没有学生 200215121 的成绩'
  PRINT @message
 END
ELSE
 BEGIN
  SET @message= '有学生 200215121 的'
  + convert(char(2),@grade_num)+ '门课程的成绩。'
  PRINT @message
 END
SET @message='课程号查询完毕'
PRINT @message
GO
{% endcodeblock %}

##  CASE 分支语句
CASE 关键字可根据表达式的真假来确定是否返回某个值，可在允许使用表达式的任意
位置使用这一关键字。
eg 为学生表的每个院系添加说明。
{% codeblock   %}
SELECT sname AS 学号,sdept AS 院系, '院系说明'=
CASE sdept
  --分别为各个院系添加说明
  WHEN 'IS' THEN '属于信息系'
  WHEN 'MA' THEN '属于数学院'
  WHEN 'CS' THEN '属于计算机科学与技术学院'
ELSE '其他院系'
END 
FROM student ORDER BY sname --按照姓名排序
{% endcodeblock %}

## WHILE 语句
设置重复执行 SQL 语句或语句块的条件。
{% codeblock   %}
WHILE 逻辑表达式
Begin
 T-SQL 语句组
[break] /*终止整个语句的执行*/
[continue] /*结束一次循环体的执行*/
END
{% endcodeblock %}

eg 求 1 到 10 之间偶数的和。
{% codeblock %}

DECLARE @i smallint,@sum smallint
SET @i=0
SET @sum=0
WHILE @i>=0
BEGIN
 SET @i=@i+1
 IF @i>10
 BEGIN
SELECT '1 到之间偶数的和'=@sum
 BREAK
 END
 IF (@i%2)!=0
 CONTINUE
 ELSE
{% endcodeblock %}

## GOTO 语句
GOTO 语句将执行语句无条件跳转到标签处，并从标签位置继续处理。GOTO 语句和标
签可在过程、批处理或语句块中的任何位置使用。其语法格式为：
GOTO label

## WAITFOR 语句
WAITFOR 语句，称为延迟语句，就是暂停执行一个指定的时间间隔或者到一个指定的时间。
{% codeblock %} 
WAITFOR 
{ 
DELAY 'time_to_pass' /* 设定等待时间 */

| TIME 'time_to_execute' /* 设定等待到某一时刻 */
}

延迟 30 秒执行查询。
WAITFOR DELAY '00:00:30'
SELECT * FROM student
{% endcodeblock %} 


## TRY-CATCH
TRY 块包含一组 T-SQL 语句。如果 TRY 块的语句中发生任何错误，控制将传递给CATCH 块。CATCH 块包含另外一组语句，这些语句在错误发生时执行。如果 TRY 块中没有错误，控制将传递到关联的 END CATCH 语句后紧跟的语句。如果 END CATCH 语句是存储过程或触发器中的最后一条语句，控制将传递到调用该存储过程或触发器的语句。

{% codeblock %} 
BEGIN TRY 
{ sql_statement | statement_block } 
END TRY
BEGIN CATCH 
{ sql_statement | statement_block } 
END CATCH [ ; ]

{% endcodeblock %} 

## Raiserror
有时会遇到 SQL SERVER 实际并不知道的一些错误，但我们希望能在客户端产生运行错误，而客户端使用的时候能够唤醒异常处理并进行相应的处理。RAISERROR 生成的错误与数据库引擎代码生成的错误的运行方式相同。

{% codeblock %} 
RAISERROR(<message ID | message_string>, <severity #级别 >,<state #状态 > [,<argument> 
[,<…n>]]) 
[WITH option[,…n]]
{% endcodeblock %}

# 游标
游标（Cursor）是一种从包括多条数据记录的结果集中每次提取一条记录以便处理的机
制，可以看做是查询结果的记录指针。
**游标的作用：**
1） 允许定位在结果集的特定行。
2） 从结果集的当前位置检索一行或一部分行。
3） 支持对结果集中当前位置的行进行数据修改。
4） 为由其他用户对显示在结果集中的数据所做的更改提供不同级别的可见性支持。
5） 提供脚本、存储过程和触发器中用于访问结果集中的数据的 T-SQL 语句。

**@@FETCH_STATUS 全局变量**返回上次执行 FETCH 命令的状态。在每次用 FETCH 从
游标中读取数据时，都应检查该变量，以确定上次 FETCH 操作是否成功，来决定如何进行
下一步处理。@@FETCH_STATUS 变量有三个不同的返回值: 1）返回值为 0，说明 FETCH 语句成功。
2）返回值为-1，说明 FETCH 语句失败或行不在结果集中。
3）返回值为-2，说明提取的行不存在。

利用游标将成绩表（SC）中不及格的成绩改为 60 分。
{% codeblock %} 
--声明变量
declare @v_sno varchar(10),
@v_cno varchar(10),@v_grade int
--声明游标
declare cur scroll cursor
for select sno,cno,grade from sc
--打开游标
open cur
--取出第一行记录
fetch next from cur into @v_sno,@v_cno,@v_grade
--循环取值
while @@FETCH_STATUS=0
begin
--判断当前记录的成绩值
if @v_grade<60
 begin 
--显示修改前的成绩
 select sno as 学号,cno as 课程号,grade as 更改前的成绩
 from sc where sno=@v_sno and cno=@v_cno
--修改游标所在行的成绩
update sc set grade=60 where current of cur
--显示修改后的成绩
 select sno as 学号,cno as 课程号,grade as 更改后的成绩
 from sc where sno=@v_sno and cno=@v_cno
 end
--取下一行记录
fetch next from cur into @v_sno,@v_cno,@v_grade
end
--关闭游标
close cur
--释放游标
deallocate cur
{% endcodeblock %}



<hr />
版权信息