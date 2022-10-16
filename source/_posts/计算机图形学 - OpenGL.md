---
title: 计算机图形学 - OpenGL  
date: 2022-10-16 20:31:12   
permalink:         
categories:  
    - 计算机图形学      
tags: 
    - 计算机图形学
    - OpenGL       
description:        
image:             
copyright: true     
---

<img src="https://" alt="" style="width:100%" />  

**前言**


OpenGL基础函数及使用模板


<!-- more -->

# OpenGL 
- 图形流水线 pic 2.23 p47
- 数据类型
![[Pasted image 20220930101710.png]]
- <GL\\glut.h>
- 函数命名规范 <库前缀><根命令><参数的数目><参数的类型>
	- 开头前缀 gl GL_
	- 数字 + 后缀  接受几个该数据类型的参数


# main 函数设置

``` C++
//设置初始窗口的位置
glutInitWindowPosition(100, 100);

    //设置初始窗口的大小
glutInitWindowSize(400, 400);

    //根据前面设置建立窗口，参数设置为变体
glutCreateWindow("实验");

    //颜色函数设置
Init();

    //绘图时被调用的函数
glutDisplayFunc(myDisplay);

    //改变窗体大小时进行图像重绘
glutReshapeFunc(Reshape);

    //进行消息循环，用于显示窗体，窗体关闭后自动退出循环
glutMainLoop();


void Reshape(int w, int h) {
    //glViewport负责把视景体截取的图像按照怎样的高和宽显示到屏幕上
    glViewport(0, 0, (GLsizei)w, (GLsizei)h);
         
    //将当前矩阵指定为投影矩阵
    glMatrixMode(GL_PROJECTION);
         
    //把矩阵设为单位矩阵
    glLoadIdentity();
         
    //让中心坐标（0，0）变成窗口的左下角
    gluOrtho2D(0.0, (GLdouble)w, 0.0, (GLdouble)h);
}


void Init(){ 
    //设置颜色 
    glClearColor(0.0, 0.0, 0.0, 0.0); 
    //颜色过渡形式
    glShadeModel(GL_FLAT); 
}
```

# 绘图函数
``` C++
void myDraw(int a, int b) {
       /*other code*/
       //指定栅格化点的直径
       glPointSize(1);
       //绘图准备
       glBegin(GL_POINTS);
       glVertex2i(/*other code*/);
       glEnd();
       }
   }

   void myDisplay(void) {
       myDraw(a,b)
       glFlush();//强制刷新缓冲，保证绘图命令将被执行
   }
```

## glBegin() 参数
| 函数              | 说明                                         |
| ----------------- | -------------------------------------------- |
| GL_POINTS         | 每个顶点作为一个点处理                       |
| GL_LINES          | 每个顶点作为一个独立线段                     |
| GL_LINE_STRIP     | 从第一个顶点到最后一个顶点依次相连的一组线段 |
| GL_LINE_LOOP      | 从第一个顶点到最后一个顶点首尾相连的一组线段 |
| GL_TRIANGLES      | 每个顶点作为一个独立的三角形                 |
| GL_TRIANGLE_STPIP | 绘制一组相连的三角形                         |
| GL_QUADS          | 绘制由四个顶点组成的一组单独的四边形         |
| GL_QUAD_STRIP     | 绘制一组相连的四边形                         |

## 可以在glBegin() 和 glEnd() 之间调用的函数
| 函数                       | 说明           |
| -------------------------- | -------------- |
| giVertex()                 | 设置顶点坐标   |
| glColor()                  | 设置当前颜色   |
| glIndex()                  | 设置当前颜色表 |
| glNormal                   | 设置法向量坐标 |
| glCoord()                  | 产生坐标       |
| glCallList(),glCallLists() | 执行显示列表   |
| glTexCoord*()              | 设置纹理坐标   |
| glEdgeFlag*()              | 控制边界绘制   |
| glMaterial*()              | 设置材质               |















# xx3x

<hr />
版权信息