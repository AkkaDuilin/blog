---
title: Java文件操作 流(Stream)、文件(File)和IO
categories:
  - Java

  - null
tags:
  - Java
  - null
copyright: true
date: 2022-02-22 17:19:12
permalink:
description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**

Java.io 包几乎包含了所有操作输入、输出需要的类。所有这些流类代表了输入源和输出目标。

Java.io 包中的流支持很多种格式，比如：基本类型、对象、本地化字符集等等。

一个流可以理解为一个数据的序列。输入流表示从一个源读取数据，输出流表示向一个目标写数据。

Java 为 I/O 提供了强大的而灵活的支持，使其更广泛地应用到文件传输和网络编程中。

<!-- more -->

# 读取控制台

## 读取输入

Java 的控制台输入由 System.in 完成
可以封装在一个BufferedReader中
BufferedReader类从字符输入流中读取文本并缓冲字符，以便有效地读取字符，数组和行
{% codeblock   %}

BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
c = (char) br.read();
System.out.println(c);

str = br.readLine();
System.out.println(str);

{% endcodeblock %}

使用 read() 方法从控制台读取一个字符，用 readLine() 方法读取一个字符串。

## 控制台输出

控制台的输出由 print( ) 和 println() 完成,print()输出完毕后不换行，而println()输出完毕后会换行，
方法都由类 PrintStream 定义，System.out 是该类对象的一个引用。

{% codeblock   %}

int b;
b = 'A';
System.out.println(b);
System.out.println('\n');

{% endcodeblock %}

# 读写文件

## FileInputStream

创建一个文件对象来创建一个输入流对象读取文件。

{% codeblock   %}
File f = new File("C:/java/hello");
InputStream in = new FileInputStream(f);
{% endcodeblock %}

相关函数

|  序号 | 方法 | 描述 |
|:-----|:-----|:-----| 
|   1   |    close()           |  关闭此文件输入流并释放与此流有关的所有系统资源     |
|   2   |    read(int r)       |  从 InputStream 对象读取指定字节的数据。返回为整数值，返回下一字节数据，如果已经到结尾则返回-1    |
|   3   |    read(byte[] r)    |  从输入流读取r.length长度的字节。返回读取的字节数。如果是文件结尾则返回-1     |


## FileOutputStream

创建一个文件并向文件中写数据。

{% codeblock   %}
OutputStream f = new FileOutputStream("C:/java/hello")
{% endcodeblock %}

相关函数

|  序号 | 方法 | 描述 |
|:-----|:-----|:-----| 
|   1  |    close()            |  关闭此文件输入流并释放与此流有关的所有系统资源     |
|   2  |    write(int w)       |  写入指定字节的数据 |
|   3  |    write(byte[] w)    |  写入w.length长度的字节     |

## 按行读取文件

{% codeblock   %}

public static void isLegalMagicSquare(String fileName) {

        try {
            File myFile = new File(fileName);//通过字符串创建File类型对象，指向该字符串路径下的文件

            if (myFile.isFile() && myFile.exists()) { //判断文件是否存在

                InputStreamReader Reader = new InputStreamReader(new FileInputStream(myFile), "UTF-8");
                //考虑到编码格式，new FileInputStream(myFile)文件字节输入流，以字节为单位对文件中的数据进行读取
                //new InputStreamReader(FileInputStream a, "编码类型")
                //将文件字节输入流转换为文件字符输入流并给定编码格式

                BufferedReader bufferedReader = new BufferedReader(Reader);
                //BufferedReader从字符输入流中读取文本，缓冲各个字符，从而实现字符、数组和行的高效读取。
                //通过BuffereReader包装实现高效读取

                String lineTxt = null;

                while ((lineTxt = bufferedReader.readLine()) != null) {
                    //buffereReader.readLine()按行读取写成字符串
                    System.out.println(lineTxt);
                }

                Reader.close();

            } else {

                System.out.println("找不到指定的文件");

            }

        } catch (Exception e) {

            System.out.println("读取文件内容出错");

            e.printStackTrace();
        }

    }

{% endcodeblock %}

# xx3x

<hr />
版权信息