---
title: 编程用笔记(更新ing)
tags: [C++]
copyright: true
date: 2021-11-08 17:33:01
permalink:
categories:
    - C++

description:
image: https://s2.loli.net/2021/12/15/2eoquz8pm6ArHMQ.jpg
---


**前言**

*收集一些经常要搜的编程小知识*
*不定期更新  ︿(￣︶￣)︿*

 <img src="https://s2.loli.net/2021/12/15/2eoquz8pm6ArHMQ.jpg" style="width:50%">

<!-- more -->

# 环境变量配置
文件夹
不要用大写
不要用大写
不要用大写

# vscode 常用快捷键

链接指路
https://blog.csdn.net/hypon2016/article/details/80831266?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522163767461216780265485668%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=163767461216780265485668&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-80831266.first_rank_v2_pc_rank_v29&utm_term=vscode%E5%BF%AB%E6%8D%B7%E9%94%AE&spm=1018.2226.3001.4187

Shift+Alt + ↓ / ↑	向上/向下复制行 Copy line up/down
Ctrl+Home	转到文件开头 Go to beginning of file
Ctrl+End	转到文件末尾 Go to end of file
Ctrl+Enter	在下面插入行 Insert line below
Ctrl+Shift+Enter	在上面插入行 Insert line above
Ctrl+Shift+\	跳到匹配的括号 Jump to matching bracket
Ctrl+Shift+K	删除行 Delete line

Ctrl+Shift+[	折叠（折叠）区域 Fold (collapse) region
Ctrl+Shift+]	展开（未折叠）区域 Unfold (uncollapse) region
Ctrl+K Ctrl+[	折叠（未折叠）所有子区域 Fold (collapse) all subregions
Ctrl+K Ctrl+]	展开（未折叠）所有子区域 Unfold (uncollapse) all subregions
Ctrl+K Ctrl+0	折叠（折叠）所有区域 Fold (collapse) all regions
Ctrl+K Ctrl+J	展开（未折叠）所有区域 Unfold (uncollapse) all regions多光标和选择 Multi-cursor and selection

Alt +单击	插入光标 Insert cursor
Ctrl + Alt +↑/↓	在上/下插入光标 Insert cursor above / below
Ctrl + U	撤消上一个光标操作 Undo last cursor operation
Shift + Alt + I	在选定的每一行的末尾插入光标 Insert cursor at end of each line selected
Shift + Alt + →	展开选择 Expand selection
Shift + Alt + ←	缩小选择 Shrink selection


# C++ 时间函数


头文件：
#include <windows.h>

{% codeblock [xxxxxx] [lang:]  %}
clock_t time_start, time_end;

/* 获取开始时间 */
time_start = GetTickCount(); //从操作系统启动经过的毫秒数

time_end = GetTickCount();

cout << "Time = " << (time_end - time_start) << "ms\n ";
{% endcodeblock %}




# C++ 随机函数


#define random(x) (rand()%x)
要取得[0,n)  就是rand（）%n     表示 从0到n-1的数

要取得[a,b)的随机整数，使用(rand() % (b-a))+ a; 
要取得[a,b]的随机整数，使用(rand() % (b-a+1))+ a; 
要取得(a,b]的随机整数，使用(rand() % (b-a))+ a + 1; 
通用公式:a + rand() % n；其中的a是起始值，n是整数的范围。 
要取得a到b之间的随机整数，另一种表示：a + (int)b * rand() / (RAND_MAX + 1)。 
要取得0～1之间的浮点数，可以使用rand() / double(RAND_MAX)。


# malloc解析


引用：
https://zhuanlan.zhihu.com/p/105090421

头文件：#include <malloc.h> 或 #include <alloc.h> (注意：alloc.h 与 malloc.h 的内容是完全一致的。)

功能：分配长度为num_bytes字节的内存块

说明：如果分配成功则返回指向被分配内存的指针，否则返回空指针NULL。

当内存不再使用时，应使用free()函数将内存块释放。

解析：
malloc的意义是向 堆区 要了一块sizeof(int) * N 这么大的空间。
返回的是指针，所以在后期使用时要解引用。

代码：
{% codeblock [malloc解析] [lang:C++]  %}
#include<stdlib.h>

int main() {

    int i = 0;
    int N = 0;
    int* arr;

    printf("请输入数组的大小\n");
    scanf("%d", &N);

    arr = (int*)malloc(sizeof(int) * N);

    printf("请输入%d个数
{% endcodeblock %}

# auto的循环用法


for(auto &a :b)

输出的结果就是0—9这十个数。

for(auto &a : arr)中“auto &a”就是变量名就和上一个for循环中的“int i”一样，

与for(int i=0;i<sizeof(arr)/sizeof(arr[0]);i++)是一样的。

{% codeblock [xxxxxx] [lang:]  %}

int arr[10];
for(int i=0;i<10;i++)
{
  arr[i]=i;
}
for(auto &a:arr)
{
  cout << a;
}
{% endcodeblock %}

**未完待续 (°ー°〃)**

<hr />
版权信息