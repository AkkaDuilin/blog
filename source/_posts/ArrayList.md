---
title: Java ArrayList
categories:
  - Java

  - null
tags:
  - Java
    - ArrayList
    - Comparator
copyright: true
date: 2022-05-23 16:01:07
permalink:
description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**

Java ArrayList 方法

sort函数的一些理解

Comparator接口的用法





<!-- more -->

# ArrayList
ArrayList是实现List接口的，底层采用数组实现。

ArrayList 实现了Cloneable接口，即覆盖了函数clone()，能被克隆。

ArrayList 实现java.io.Serializable接口，这意味着ArrayList支持序列化，能通过序列化去传输。

头文件
import java.util.ArrayList;

# 方法

https://blog.csdn.net/ly0724ok/article/details/117966154/

<a href="https://sm.ms/image/fOX4cxyuBvkgrKb" target="_blank"><img src="https://s2.loli.net/2022/05/23/fOX4cxyuBvkgrKb.png" ></a>

# sort自定义排序

方法原型
void java.util.ArrayList.sort(Comparator<? super Contury> c)

Comparator接口具有比较的功能，接口注重容器
而Comparator接口中必须要实现的compare(T o1,T o2)有两个参数

**在数组sort中实现Comparator接口的重写**
{% codeblock   %}
table.sort( new Comparator<Contury>() {
  @Override
  // compare重写
  public int compare(Contury c1,Contury c2){
      if(c1.gold>c2.gold){
          return 0;
      }
      else return -1;
  }
});
{% endcodeblock %}

**直接重写Comparator接口**
{% codeblock   %}
class StudentComparator implements Comparator<Student>{  
    @Override  
    public int compare(Student o1, Student o2) {  
        // TODO Auto-generated method stub  
        if(o1.getScore()>o2.getScore())  
            return -1;  
        else if(o1.getScore()<o2.getScore())  
            return 1;  
        else{  
            if(o1.getAge()>o2.getAge())  
                return 1;  
            else if(o1.getAge()<o2.getAge())  
                return -1;  
            else   
                return 0;  
        }  
    }  
      
}  
{% endcodeblock %}

https://blog.51cto.com/u_15338614/3582482

# xx3x

<hr />
版权信息