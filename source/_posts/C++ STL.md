---
title: C++ STL 
date: 2022-11-27 11:35:04   
permalink:         
categories:  
    - C++
    - STL
    -       
tags: 
    - C++
    - STL        
description:        
image:             
copyright: true     
---

<img src="https://" alt="" style="width:100%" />  

**前言**





<!-- more -->

# 栈和队列
## 基础知识
[[栈和队列]]

## 双向队列
- deque双向队列是一种双向开口的连续线性空间，可以高效的在头尾两端插入和删除元素
![[Pasted image 20221127142948.png]]
## 优先级队列
http://www.cppblog.com/shyli/archive/2007/04/06/21366.html
- priority_queue 优先级队列是一个拥有权值概念的单向队列，在这个队列中，所有元素是按优先级排列的（也可以认为queue是个按进入队列的先后做为优先级的优先级队列——先进入队列的元素优先权要高于后进入队列的元素）。

- 在STL的具体实现中，priority_queue也是以别的容器作为底部结构，再根据堆的处理规则来调整元素之间的位置。

- 优先级高的元素先出队列

```C++
#include<iostream>
#include<vector>
#include<queue>
#include<functional>
 
using namespace std;

struct Node{
	friend bool operator < (node n1,node n2)
	{
		return n1.key < n2.key;
	}
	int key;
	int value;
}
 
int main()
{
 
    const int len = 5;
    int i;
    int a[len] = {3,5,9,6,2};
    priority_queue<int> qi;
    for(i = 0; i < len; i++)
        qi.push(a[i]);
    for(i = 0; i < len; i++)
    {
        cout<<qi.top()<<" ";
        qi.pop();
    }
    cout<<endl;
 
 
    priority_queue<Node> pq2;
    //priority_queue<Node,vector<Node>,cmpLess> pq2;
    Node b[len];
    b[0].key = 6; b[0].value = 1;
    b[1].key = 9; b[1].value = 5;
    b[2].key = 2; b[2].value = 3;
    b[3].key = 8; b[3].value = 2;
    b[4].key = 1; b[4].value = 4;
 
    for(i = 0; i < len; i++)
        pq2.push(b[i]);
    cout<<"优先级"<<'\t'<<"值"<<endl;
    for(i = 0; i < len; i++)
    {
        cout<<pq2.top().key<<'\t'<<pq2.top().value<<endl;
        pq2.pop();
    }
    return 0;
}
```
# Map
- 关联容器，提供一对一的hash
- 自动建立 key - value 的对应 key和value可以是任意类型
## 构造函数
```C++
map<int, string> mapStudent; 
```

## 插入元素
```C++
// 第一种 用insert函數插入pair 
mapStudent.insert(pair<int, string>(000, "student_zero")); 

// 第二种 用insert函数插入value_type数据 
mapStudent.insert(map<int,string>::value_type(001,"student_one"));

// 第三种 用"array"方式插入 
mapStudent[123] = "student_first";

```

## 查找元素
```C++
iter = mapStudent.find("123");
```
- 若找到key对应的value 返回数据所在对象位置
- 若没找到 返回对于map::end() 位置

## 删除/清空
```C++
//迭代器刪除 
iter = mapStudent.find("123"); mapStudent.erase(iter); 

//用关键字刪除 
int n = mapStudent.erase("123"); //如果刪除了會返回1，否則返回0 

//用迭代器范围刪除 : 把整个map清空 
mapStudent.erase(mapStudent.begin(), mapStudent.end());
```

| 函数            | 功能                            |
| --------------- | ------------------------------- |
| begin()         | 返回指向map头部的迭代器         |
| clear(）        | 删除所有元素                    |
| count()         | 返回指定元素出现的次数          |
| empty()         | 如果map为空则返回true           |
| end()           | 返回指向map末尾的迭代器         |
| equal_range()   | 返回特殊条目的迭代器对          |
| erase()         | 删除一个元素                    |
| find()          | 查找一个元素                    |
| get_allocator() | 返回map的配置器                 |
| insert()        | 插入元素                        |
| key_comp()      | 返回比较元素key的函数           |
| lower_bound()   | 返回键值>=给定元素的第一个位置  |
| max_size()      | 返回可以容纳的最大元素个数      |
| rbegin()        | 返回一个指向map尾部的逆向迭代器 |
| rend()          | 返回一个指向map头部的逆向迭代器 |
| size()          | 返回map中元素的个数             |
| swap()          | 交换两个map                     |
| upper_bound()   | 返回键值>给定元素的第一个位置   |
| value_comp()    | 返回比较元素value的函数         |

## 哈希表
https://blog.csdn.net/u010025211/article/details/46653519

- hash_map基于[hash](https://so.csdn.net/so/search?q=hash&spm=1001.2101.3001.7020) table（哈希表）。 哈希表最大的优点，就是把数据的存储和查找消耗的时间大大降低，几乎可以看成是常数时间；而代价仅仅是消耗比较多的内存。然而在当前可利用内存越来越多的情况下，用空间换时间的做法是值得的。另外，编码比较容易也是它的特点之一。

- 其基本原理是：使用一个下标范围比较大的数组来存储元素。可以设计一个函数（[哈希](https://so.csdn.net/so/search?q=%E5%93%88%E5%B8%8C&spm=1001.2101.3001.7020)函数，也叫做散列函数），使得每个元素的关键字都与一个函数值（即数组下标，hash值）相对应，于是用这个数组单元来存储这个元素；也可以简单的理解为，按照关键字为每一个元素“分类”，然后将这个元素存储在相应“类”所对应的地方，称为桶。

| 函数     | 功能 |
| -------- | ---- |
| at()     |      |
| begin()  |      |
| size()   |      |
| clear()  |      |
| swap()   |      |
| find()   |      |
| insert() |      |
| erase()  |      |
|          |      |


# 堆

# xx3x

<hr />
版权信息