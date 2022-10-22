---
title: 矩阵乘法Strassen算法 
date: 2022-10-19 19:43:40   
permalink:         
categories:  
    - 算法
    -
    -       
tags: 
    - 算法
    - 分治        
description:        
image:             
copyright: true     
---

<img src="https://" alt="" style="width:100%" />  

**前言**

矩阵乘法Strassen算法

参考博客：
https://www.jianshu.com/p/6e21f8e872fd
https://blog.csdn.net/yangtzhou/article/details/105042627


<!-- more -->

# 矩阵乘法Strassen算法
## 背景
一般的矩阵乘法需要O(n^3) 
三层循环

```java
SQUARE-MATRIX-MULTIPLY(A, B)
n = A.rows
let C be a new nxn matrix
for i = 1 to n
    for j = 1 to n
        c[i][j] = 0
        for k = 1 to n
            c[i][j] += a[i][k] * b[k][j]
return C
```

## 解决方法

把每个矩阵分割为4份
![[Pasted image 20221019195524.png]]
然后创建如下10个中间矩阵：

S1 = B12 - B22  
S2 = A11 + A12  
S3 = A21 + A22  
S4 = B21 - B11  
S5 = A11 + A22  
S6 = B11 + B22  
S7 = A12 - A22  
S8 = B21 + B22  
S9 = A11 - A21  
S10 = B11 + B12

接着，计算7次矩阵乘法：

P1 = A11 • S1  
P2 = S2 • B22  
P3 = S3 • B11  
P4 = A22 • S4  
P5 = S5 • S6  
P6 = S7 • S8  
P7 = S9 • S10

C11 = P5 + P4 - P2 + P6  
C12 = P1 + P2  
C21 = P3 + P4  
C22 = P5 + P1 - P3 - P7

由上可得次算法需要递归7次，所以递归式为
  ![[Pasted image 20221019195824.png]]


![[Pasted image 20221019201057.png]]
# 代入法求解递归式

<hr />
版权信息