---
title: matlab笔记
categories:
  - matlab

tags:
  - matlab
copyright: true
date: 2022-01-17 11:17:51
permalink:
description:
image:
---

<a href="https://sm.ms/image/pstS2TFVXGEo71x" target="_blank"><img src="https://s2.loli.net/2022/01/17/pstS2TFVXGEo71x.jpg" ></a>

**前言**

matlab笔记，备战美赛

冲鸭！！！



<!-- more -->

# 基础知识

## 矩阵和数组
所有 MATLAB 变量都是多维数组，与数据类型无关。矩阵是指通常用来进行线性代数运算的二维数组。

### 数组创建
1. 用空格或者逗号(,)分隔数据
a = [1 2 3 4]
2. 用分号;分隔多行数据
a = [1 3 5; 2 4 6; 7 8 10]
3. 创建矩阵的另一种方法是使用 ones、zeros 或 rand 等函数。
zeros全部为零

ones全部为 1

rand均匀分布的随机元素

randn正态分布的随机元素

z = zeros(5,1)

### 运算
1. 用单一运算符处理矩阵中的所有值
<a href="https://sm.ms/image/uTdrzlhOf4jVIJq" target="_blank"><img src="https://s2.loli.net/2022/01/17/uTdrzlhOf4jVIJq.jpg" style="width:60%"></a>

2. 转置矩阵使用单引号
a'
撇号运算符（例如，A'）执行复共轭转置。它会围绕主对角线翻转矩阵，并且还会更改矩阵的任何复数元素的虚部符号。点撇号运算符 (A.') 转置矩阵，但不会影响复数元素的符号。对于包含所有实数元素的矩阵，这两个运算符返回相同结果。

3. inv()
计算方阵x的逆矩阵

4. 使用 * 执行矩阵乘法
<a href="https://sm.ms/image/aZrP1lmifzCGKJM" target="_blank"><img src="https://s2.loli.net/2022/01/17/aZrP1lmifzCGKJM.jpg" style="width:60%" ></a>

5. 使用 format 命令可以显示更多小数位数
format long
format short

6. 执行元素级乘法 .* 运算符
乘法、除法和幂的矩阵运算符分别具有执行元素级运算的对应数组运算符。

7. 串联
连接数组以便形成更大数组的过程，成对的方括号 [] 即为串联运算符。
<a href="https://sm.ms/image/QPu2vlSCEnIe15g" target="_blank"><img src="https://s2.loli.net/2022/01/17/QPu2vlSCEnIe15g.jpg" style="width:60%"></a>

8. 复数
表示虚部用 i j 
c = [3+4i, 4+3j; -i, 10j]
c = 2×2 complex

   3.0000 + 4.0000i   4.0000 + 3.0000i
   0.0000 - 1.0000i   0.0000 +10.0000i

9. sum()
S = sum(A) 返回 A 沿大小不等于 1 的第一个数组维度的元素之和。

如果 A 是向量，则 sum(A) 返回元素之和。

如果 A 是矩阵，则 sum(A) 将返回包含每列总和的行向量。

如果 A 是多维数组，则 sum(A) 沿大小不等于 1 的第一个数组维度计算，并将这些元素视为向量。此维度会变为 1，而所有其他维度的大小保持不变。

S = sum(A,dim) 沿维度 dim 返回总和。例如，如果 A 为矩阵，则 sum(A,2) 是包含每一行总和的列向量。

S = sum(A,'all') 计算 A 的所有元素的总和。

使用 sum 和 diag 函数可以获取主对角线上的元素的总和：

sum(diag(A))


### 索引

A = 4×4

     1     2     3     4
     5     6     7     8
     9    10    11    12
    13    14    15    16

1. 指定行和列下标
A(4,2)
ans = 14

2. 单一下标按顺序向下遍历每一列
A(8)
ans = 14

3. 要引用多个数组元素，请使用冒号运算符，这使您可以指定一个格式为 start:end 的范围
A(1:3,2)
ans = 3×1

     2
     6
    10
单独的冒号（没有起始值或结束值）指定该维中的所有元素。
A(3,:)
ans = 1×5

     9    10    11    12 
冒号运算符还允许您使用较通用的格式 start:step:end 创建等间距向量值。默认步长为1
B = 0:10:100
B = 1×11

     0    10    20    30    40    50    60    70    80    90   100

4. 包含冒号的下标表达式引用部分矩阵：
A(1:k,j)
表示 A 第 j 列中的前 k 个元素。因此，
sum(A(1:4,4)) 计算第四列的总和。
但是，执行此计算有一种更好的方法。冒号本身引用矩阵行或列中的所有元素，而关键字 end 引用最后一个行或列。
sum(A(:,end))

5. 删除行和列
只需使用一对方括号即可从矩阵中删除行和列。首先
X = A
然后，要删除 X 的第二列，请使用
X(:,2) = []
这会将 X 更改为
X =
    16     2    13
     5    11     8 
     9     7    12
     4    14     1
如果您删除矩阵中的单个元素，结果将不再是矩阵。因此，以下类似表达式
  X(1,2) = []
将会导致错误。
但是，使用单一下标可以删除一个元素或元素序列，并将其余元素重构为一个行向量。因此
X(2:2:10) = []
生成
X =
    16     9     2     7    13    12     1

### 结构体
结构体是多维 MATLAB 数组，包含可按文本字段标志符访问的元素。例如，
S.name = 'Ed Plum';
S.score = 83;
S.grade = 'B+'
创建一个具有三个字段的标量结构体：
S = 
     name: 'Ed Plum'
    score: 83
    grade: 'B+'
与 MATLAB 环境中的所有其他内容一样，结构体也为数组，因此可以插入其他元素。在本示例中，数组的每个元素都是一个具有若干字段的结构体。可以一次添加一个字段，
S(2).name = 'Toni Miller';
S(2).score = 91;
S(2).grade = 'A-';
也可以使用一个语句添加整个元素：
S(3) = struct('name','Jerry Garcia',... 'score',70,'grade','C')

## 工作区变量 
使用 
whos 查看工作区内容
save 保存数据 系统使用.mat拓展名将工作区保存在当前工作文件夹中一个名为 MAT 文件的压缩文件中
load 还原到工作区
https://ww2.mathworks.cn/help/matlab/learn_matlab/workspace.html

## 字符串和文本
处理文本时，将字符序列括在双引号中
strlength 函数求数组中每个字符串的长度
是个数组，每个元素包含单个字符
https://ww2.mathworks.cn/help/matlab/learn_matlab/character-strings.html

## 函数
输入参数括在圆括号

存在多个输入参数，请使用逗号加以分隔

存在多个输出参数，请将其括在方括号中
[maxA,location] = max(A)
maxA = 5
location = 3

字符输入括在单引号中

有关初等数学函数的列表，请键入

help elfun
有关更多高等数学函数和矩阵函数的列表，请键入

help specfun
help elmat

## 运算符

### 矩阵运算符
表达式使用大家熟悉的算术运算符和优先法则。

+ 加法

- 减法

* 乘法

/ 除法

\ 左除

^ 幂

' 复共轭转置

( )指定计算顺序

### 数组运算符
如果矩阵不用于线性代数运算，则成为二维数值数组。数组的算术运算按元素执行。这意味着，加法和减法运算对数组和矩阵都是相同的，但乘法运算不相同。MATLAB 的乘法数组运算表示法中包含点，也就是小数点。

运算符列表包括

+ 加法

- 减法

.* 逐元素乘法

./ 逐元素除法

.\ 逐元素左除

.^ 逐元素幂

.' 非共轭数组转置

### 构建表
数组运算对构建表非常有用。假定 n 为列向量

n = (0:9)';
然后，

pows = [n  n.^2  2.^n]
构建一个平方和 2 次幂的表：

pows =
     0     0     1
     1     1     2
     2     4     4
     3     9     8
     4    16    16
     5    25    32
     6    36    64
     7    49   128
     8    64   256
     9    81   512

### 常用常量值
pi 3.14159265...

i 虚数单位 

j 与 i 相同

eps 浮点相对精度 ε=2^−52

realmin 最小浮点数 2^−1022

realmax 最大浮点数 (2−ε)2^1023

Inf 无穷

NaN 非数字

## 二维图和三维图
https://ww2.mathworks.cn/help/matlab/learn_matlab/basic-plotting-functions.html#responsive_offcanvas

### 线图
要创建二维线图，请使用 plot 函数
plot(x,y,'r--')

x 数据范围
x = 0:pi/100:2*pi;
*0到2pi，中间以pi/100为间距取点*
*x分别取0，pi/100,2pi/100,3pi/100.......2pi*

y 函数
y = sin(x);

'r--' 线条设定。每个设定可包含表示线条颜色、样式和标记的字符。

默认情况下，每次调用绘图函数、重置坐标区及其他元素以准备新绘图时，MATLAB® 都会清空图窗。

要将绘图添加到现有图窗中，请使用 hold on。在使用 hold off 或关闭窗口之前，当前图窗窗口中会显示所有绘图。

### 三维绘图
surf(X,Y,Z)
z = f (x,y)
要计算 z，请首先使用 meshgrid 在此函数的域中创建一组 (x,y) 点。

[X,Y] = meshgrid(-2:.2:2);  
*.2表示0.2 (-2:.2:2)表示在-2到2的区间上以0.2的长度为间隔的向量*                              
Z = X .* exp(-X.^2 - Y.^2);
然后，创建曲面图。

surf(X,Y,Z)
surf 函数及其伴随函数 mesh 以三维形式显示曲面图。surf 使用颜色显示曲面图的连接线和面。mesh 生成仅以颜色标记连接定义点的线条的线框曲面图。

### 子图
subplot 函数可以在同一窗口的不同子区域显示多个绘图
subplot 的前两个输入表示每行和每列中的绘图数。第三个输入指定绘图是否处于活动状态。



## 编程和脚本

### 基本语言 
1. 创建脚本
edit name

2. 注释 %

3. 运行脚本 输入当前脚本名称

### 实时脚本
要使用 edit 命令创建新的实时脚本，请在文件名中包含 .mlx 扩展名：

edit newfile.mlx

### 循环和条件语句
{% codeblock [xxxxxx] [lang:]  %}
N = 100;
f(1) = 1;
f(2) = 1;
%循环%
for n = 3:N
    f(n) = f(n-1) + f(n-2);
end
f(1:10)
%条件%
num = randi(100)
if num < 34
   sz = 'low'
elseif num < 67
   sz = 'medium'
else
   sz = 'high'
end


{% endcodeblock %}





# 函数总结

## magic(n)
M = magic(n) 返回由 1 到 n2 的整数构成并且总行数和总列数相等的 n×n 矩阵。n 的阶数必须是大于或等于 3 的标量才能创建有效的幻方矩阵。

## inv()
Y = inv(X) 计算方阵 X 的 逆矩阵。

## clc 
clc 函数清空命令行窗口。

##  meshgrid(x,y)
语法

[X,Y] = meshgrid(x,y)
[X,Y] = meshgrid(x)
[X,Y,Z] = meshgrid(x,y,z)
[X,Y,Z] = meshgrid(x)

说明
[X,Y] = meshgrid(x,y) 基于向量 x 和 y 中包含的坐标返回二维网格坐标。X 是一个矩阵，每一行是 x 的一个副本；Y 也是一个矩阵，每一列是 y 的一个副本。坐标 X 和 Y 表示的网格有 length(y) 个行和 length(x) 个列。

[X,Y] = meshgrid(x) 与 [X,Y] = meshgrid(x,x) 相同，并返回网格大小为 length(x)×length(x) 的方形网格坐标。

[X,Y,Z] = meshgrid(x,y,z) 返回由向量 x、y 和 z 定义的三维网格坐标。X、Y 和 Z 表示的网格的大小为 length(y)×length(x)×length(z)。

[X,Y,Z] = meshgrid(x) 与 [X,Y,Z] = meshgrid(x,x,x) 相同，并返回网格大小为 length(x)×length(x)×length(x) 的三维网格坐标。

## exp(x)
Y = exp(X) 为数组 X 中的每个元素返回指数 ex。 

## cylinder()
创建圆柱
[X,Y,Z] = cylinder 返回三个 2×21 矩阵，其中包含圆柱的 x、y 和 z 坐标，但不对其绘图。圆柱的半径为 1，圆周上有 20 个等间距点。底面平行于 xy 平面。

要绘制圆柱，请将 X、Y 和 Z 传递给 surf 或 mesh 函数。
https://ww2.mathworks.cn/help/matlab/ref/cylinder.html?searchHighlight=cylinder&s_tid=srchtitle_cylinder_1

<hr />
版权信息