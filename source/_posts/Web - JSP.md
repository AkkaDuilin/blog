---
title: Web - JSP
date: 2022-11-23 16:47:39   
permalink:         
categories:  
    - Web开发
    -
    -       
tags: 
    - Web开发
    - JSP
    - 前端
description:        
image:             
copyright: true     
---

<img src="https://" alt="" style="width:100%" />  

**前言**

JSP全称Java Server Pages，是一种动态网页开发技术。它使用JSP标签在HTML网页中插入Java代码。标签通常以<%开头以%>结束。

JSP是一种Java servlet，主要用于实现Java web应用程序的用户界面部分。网页开发者们通过结合HTML代码、XHTML代码、XML元素以及嵌入JSP操作和命令来编写JSP。

JSP通过网页表单获取用户输入数据、访问数据库及其他数据源，然后动态地创建网页。

JSP标签有多种功能，比如访问数据库、记录用户选择信息、访问JavaBeans组件等，还可以在不同的网页中传递控制信息和共享信息。



<!-- more -->

# 生命周期
-   **编译阶段：**
    
    servlet容器编译servlet源文件，生成servlet类
    
-   **初始化阶段：**
    
    加载与JSP对应的servlet类，创建其实例，并调用它的初始化方法
    
-   **执行阶段：**
    
    调用与JSP对应的servlet实例的服务方法
    
-   **销毁阶段：**
    
    调用与JSP对应的servlet实例的销毁方法，然后销毁servlet实例

# 语法

## 语法格式
`<% 代码片段 %>`

```jsp
<jsp:scriptlet>
   代码片段
</jsp:scriptlet>
```

## 中文编码
- 文件头部添加
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"pageEncoding="UTF-8"%>
```

## 声明

```jsp
<%! declaration; [ declaration; ]+ ... %>

<%! int i = 0; %> 
<%! int a, b, c; %> 
<%! Circle a = new Circle(2.0); %>
```

## 表达式

```jsp
<%= 表达式 %>

<p>
   今天的日期是: <%= (new java.util.Date()).toLocaleString()%>
</p>
```

## 控制流语句示例

### 判断
```jsp
<% if (day == 1 || day == 7) { %>
      <p>今天是周末</p>
<% } else { %>
      <p>今天不是周末</p>
<% } %>
```

### while
```jsp
<%while ( fontSize <= 3){ %>
   <font color="green" size="<%= fontSize %>">
    菜鸟教程
   </font><br />
<%fontSize++;%>
<%}%>
```

### switch
```jsp
<% 
switch(day) {
case 0:
   out.println("星期天");
   break;
case 1:
   out.println("星期一");
   break;
case 2:
   out.println("星期二");
   break;
case 3:
   out.println("星期三");
   break;
case 4:
   out.println("星期四");
   break;
case 5:
   out.println("星期五");
   break;
default:
   out.println("星期六");
}
%>
```

### for
```jsp
<%for ( fontSize = 1; fontSize <= 3; fontSize++){ %>
   <font color="green" size="<%= fontSize %>">
    菜鸟教程
   </font><br />
<%}%>
```


# 指令

| 指令                  | 描述 |
| ------------------   | ---- |
| `<%@ page ... %>  `    |  定义网络属性    |
|` <%@ include ... %> `  |    包含其他文件  |
|` <%@ taglib ... %>   ` |   引入标签库的定义   |


### page属性
| 属性                  | 描述 |
| ------------------   | ---- |
|buffer|指定out对象使用缓冲区的大小|
|autoFlush|控制out对象的 缓存区|
|contentType|指定当前JSP页面的MIME类型和字符编码|
|errorPage|指定当JSP页面发生异常时需要转向的错误处理页面|
|isErrorPage|指定当前页面是否可以作为另一个JSP页面的错误处理页面|
|extends|指定servlet从哪一个类继承|
|import|导入要使用的Java类|
|info|定义JSP页面的描述信息|
|isThreadSafe|指定对JSP页面的访问是否为线程安全|
|language|定义JSP页面所用的脚本语言，默认是Java|
|session|指定JSP页面是否使用session|
|isELIgnored|指定是否执行EL表达式|
|isScriptingEnabled|确定脚本元素能否被使用|

# 动作元素

## 格式
```jsp
<jsp:action_name attribute="value" />
```

| 语法            | 描述                           |
| --------------- | ------------------------------ |
| jsp:include     | 在页面被请求的时候引入一个文件 |
| jsp:useBean     |实例化一个JavaBean                                |
| jsp:setProperty |    设置JavaBean                            |
| jsp:getProperty |     输出JavaBEan属性                           |
| jsp:forward     |     将请求转到新页面                           |
| jsp:element     |      定义动态XML元素                          |
| jsp:attribute   |      设置动态XML元素属性             |
| jsp:body        |       设置动态XML元素内容                         |
| jsp:text        |       使用写入文本的模板                         |


## jsp:include 
```jsp
<jsp:include page="相对 URL 地址" flush="true" />
```


## jsp:forward
```jsp
<jsp:forward page="相对 URL 地址" />
```

##  <jsp:element> 、 <jsp:attribute>、 <jsp:body>动作元素
```jsp
<jsp:element name="xmlElement">
<jsp:attribute name="xmlElementAttr">
   属性值
</jsp:attribute>
<jsp:body>
   XML 元素的主体
</jsp:body>
</jsp:element>
```


# 客户端/服务器

##  HttpServletRequest

request对象是javax.servlet.http.HttpServletRequest类的实例。每当客户端请求一个页面时，JSP引擎就会产生一个新的对象来代表这个请求。

request对象提供了一系列方法来获取HTTP信息头，包括表单数据，cookies，HTTP方法等等。

###  getCookies()
- 返回客户端所有的Cookie数组

### getAttributeNames()
- 返回request对象的所有属性名称的集合

### getHeaderNames()
- 返回所有HTTP头的名称集合

### 示例
```jsp
<%
   Enumeration headerNames = request.getHeaderNames();
   while(headerNames.hasMoreElements()) {
      String paramName = (String)headerNames.nextElement();
      out.print("<tr><td>" + paramName + "</td>\n");
      String paramValue = request.getHeader(paramName);
      out.println("<td> " + paramValue + "</td></tr>\n");
   }
%>
```

## HttpServletResponse
Response响应对象主要将JSP容器处理后的结果传回到客户端。可以通过response变量设置HTTP的状态和向客户端发送数据，如Cookie、HTTP文件头信息等。


### void addCookie(Cookie cookie)
- 添加指定的cookie至响应中

### 
# xx3x

<hr />
版权信息