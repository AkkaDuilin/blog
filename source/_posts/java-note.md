---
title: Java 学习笔记(基础篇)
categories:
  - Java

  - null
tags:
  - Java
  - null
copyright: true
date: 2022-02-21 11:04:51
permalink:
description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**

Java 学习笔记(基础篇)

2022.2.21 

持续更新


<!-- more -->

# 内置数据结构
1. byte
最小值是 -128（-2^7）；
最大值是 127（2^7-1）；
默认值是 0；

2. short
最小值是 -32768（-2^15）；
最大值是 32767（2^15 - 1）；
Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
默认值是 0；

3. int
最小值是 -2,147,483,648（-2^31）；
最大值是 2,147,483,647（2^31 - 1）；
一般地整型变量默认为 int 类型；
默认值是 0 ；

4. long
最小值是 -9,223,372,036,854,775,808（-2^63）；
最大值是 9,223,372,036,854,775,807（2^63 -1）；
这种类型主要使用在需要比较大整数的系统上；
默认值是 0L；

5. float
float 数据类型是单精度. 32位. 符合IEEE 754标准的浮点数；
float 在储存大型浮点数组的时候可节省内存空间；
默认值是 0.0f；

5. double：
double 数据类型是双精度. 64 位. 符合 IEEE 754 标准的浮点数；
浮点数的默认类型为 double 类型；
double类型同样不能表示精确的值，如货币；
默认值是 0.0d；

6. boolean
1 = true
0 = false
默认值为false

7. char
储存任何字符



# 变量
1. 声明变量
type identifier [ = value][, identifier [= value] ...] ;

2. 局部变量
局部变量声明在方法. 构造方法或者语句块中；

局部变量在方法. 构造方法. 或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；

局部变量只在声明它的方法. 构造方法或者语句块中可见；

3. 静态变量
类变量也称为静态变量，在类中以 static 关键字声明，但必须在方法之外。

无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。

静态变量除了被声明为常量外很少使用，静态变量是指声明为 public/private，final 和 static 类型的变量。静态变量初始化后不可改变。

静态变量储存在静态存储区。经常被声明为常量，很少单独使用 static 声明变量。

静态变量在第一次被访问时创建，在程序结束时销毁。

静态变量可以通过：ClassName.VariableName的方式访问

4. 实例变量
实例变量声明在一个类中，但在方法. 构造方法和语句块之外；

当一个对象被实例化之后，每个实例变量的值就跟着确定；

实例变量在对象创建的时候创建，在对象被销毁的时候销毁；

实例变量的值应该至少被一个方法. 构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；

实例变量可以声明在使用前或者使用后；

。

# 修饰符

## 访问控制修饰符

public protected default private

## 非访问修饰符

static 声明独立于对象的静态变量或者静态方法

final 变量一旦赋值后，不能被重新赋值
父类的final方法可以被子类继承，但不能被重写，final类不能被继承

abstract 
抽象类不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充。
抽象方法是一种没有任何实现的方法，该方法的具体实现由子类提供。

synchronized  
关键字声明的方法同一时间只能被一个线程访问。synchronized 修饰符可以应用于四个访问修饰符。

transient 

volatile

# 三目运算符
variable x = (expression) ? value if true : value if false

# 循环语句

同C++写法

while( 布尔表达式 ) {
  //循环内容
}

do {
       //代码语句
}while(布尔表达式);

for(初始化; 布尔表达式; 更新) {
    //代码语句
}

break

continue



**增强for循环** 主要用于数组

for(声明语句 : 表达式)
{
   //代码句子
}

{% codeblock [xxxxxx] [lang:]  %}
public class Test {
   public static void main(String[] args){
      int [] numbers = {10, 20, 30, 40, 50};
 
      for(int x : numbers ){
         System.out.print( x );
         System.out.print(",");
      }
      System.out.print("\n");
      String [] names ={"James", "Larry", "Tom", "Lacy"};
      for( String name : names ) {
         System.out.print( name );
         System.out.print(",");
      }
   }
}
{% endcodeblock %}

# 条件语句
{% codeblock [xxxxxx] [lang:]  %}
if(布尔表达式 1){
   //如果布尔表达式 1的值为true执行代码
}else if(布尔表达式 2){
   //如果布尔表达式 2的值为true执行代码
}else if(布尔表达式 3){
   //如果布尔表达式 3的值为true执行代码
}else {
   //如果以上布尔表达式都不为true执行代码
}

switch(expression){
    case value :
       //语句
       break; //可选
    case value :
       //语句
       break; //可选
    //你可以有任意数量的case语句
    default : //可选
       //语句
}

{% endcodeblock %}

# Math 类

|  序号 | 方法 | 描述 |
|:-----|:-----|:-----|
|   1   | xxxValue() | 将 Number 对象转换为xxx数据类型的值并返回。|
|   2   | equals() | 判断number对象是否与参数相等 |
|   3   | valueOf() | 返回Number对象指定的内置数据类型 |
|   4   | parseInt() | 将字符串解析为int类 |
|   5   | toString() | 以字符串形式返回值|
|   6   | abs() | 返回参数的绝对值 | 
|   7   | ceil() | 返回大于等于给定参数的最小整数 |
|   8   | floor() | 返回小于等于给定参数的最大整数 |
|   9   | rint() | 返回与参数最接近的整数 | 
|   10  | round() | 四舍五入 |
|   11  | max()/min() | 返回两个参数的最大/小值 |
|   12  | exp() | 返回参数的自然数底数的对数值 |
|   13  | log() | 返回参数的自然数底数的对数值 |
|   14  | pow() | x.pow(y) 返回 x的y次方 |
|   15  | sqrt() | 求算术平方根 |
|   16  | cos()/tan()/sin()/asin()| 三角函数相关 |
|   17  | random() | 返回一个随机数 |

# Character类 

|  序号 | 方法 | 描述 |
|:-----|:-----|:-----|
|  1  |  isLetter() | 是否为字母 |
|  2  |  isDigit()  |  是否为数字字符 |
|  3  |  isWhitespace() |  是否为空白字符 |
|  4  |  isUpperCase()/isLowerCase()  |  是否为大写/小写  |
|  5  |  toUpperCase()/toLowerCase()   |  转换为大写/小写   |

# String类
https://www.runoob.com/java/java-string.html

|  序号 | 方法 | 描述 |
|:-----|:-----|:-----|
|  1  |  charAt(int index) |  返回指定索引处的char值  |
|  2  |  compareTo(String str)   |  按字典顺序比较字符串 *Tip1 |
|  3  |  concat(String str)   |  将指定字符串str连接到字符串末尾  |
|  4  |  endWith(startsWith)(String suffix)  |  是否以指定后缀结束(开始)   |
|  5  |  equals(Object anObject) |  比较两个字符串的内容是否相等  |
|  6  |  indexOf(int ch(String str)， int fromIndex)  |  返回指定字符在此字符串中第一次出现处的索引,从指定位置开始  |
|  7  |  lastIndexOf(int ch, int fromIndex)  |  返回指定字符在此字符串中最后一次出现处的索引,从指定位置开始 |
|  8  |  length() |  返回字符串的长度  |
|  9  |  replace(char old, char new)   |  返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的   |
|  10 |  replaceAll(replaceFirst)(String regex, String replacement) |  使用给定的 replacement 替换此字符串所有(第一个)匹配给定的正则表达式的子字符串   |
|  11 |  split(String regex)  |  根据给定正则表达式的匹配拆分此字符串   |
|  12 |  substring(int beginIndex, int endIndex)   |  返回字符串的子字符串 *Tip2|
|  13 |  toUpperCase(toLowerCaes)(Locale locale)   |  将字符串小(大)写字符转换为大(小)写  |
|  14 |  toCharArray()  |  将此字符串转换为一个新的字符数组 |
|  15 |  isEmpty()   |  判断字符串是否为空   |


Tip1: 如果参数字符串等于此字符串，则返回值 0
如果此字符串小于字符串参数，则返回一个小于 0 的值；
如果此字符串大于字符串参数，则返回一个大于 0 的值。

Tip2:
beginIndex -- 起始索引（包括）, 索引从 0 开始。
endIndex -- 结束索引（不包括）

## 判断字符串是否包含特殊字符 

{% codeblock [xxxxxx] [lang:]  %}

 public static boolean isSpecialChar(String str) {
        String regEx = "[ _`~!@#$%^&*()+=|{}':;',\\[\\].<>/?~！@#￥%……&*（）——+|{}【】‘；：”“’。，. ？]|\n|\r|\t";
        Pattern p = Pattern.compile(regEx);
        Matcher m = p.matcher(str);
        return m.find();
    }

{% endcodeblock %}

# Integer类
可以在数据转换时使用
Interger做为一个包装类型或者说是一个引用类型的,可以传null
**常用方法**

1. Integer(int value)和Integer(String s)
构造方法，肯定常用。

2. public static int parseInt(String s)
将字符串转换成整数。

3. public static String toBinaryString(int i)
将一个正整数转换成2进制字符串。

public static String toOctalString(int i)
将一个正整数转换成8进制字符串。

public static String toHexString(int i)
将一个正整数转换成16进制字符串。

public static String toUnsignedString(int i, int radix)
将一个正整数转换成r进制字符串（r的范围是[2, 64]）。

4. public static Integer valueOf(int i)
将一个整数转换成Integer类型对象，即装箱。

public static Integer valueOf(String s)
将字符串数字转换成Integer类型对象，也是装箱。



# StringBuffer 和 StringBuilder

https://www.runoob.com/manual/jdk11api/java.base/java/lang/StringBuilder.html
https://www.runoob.com/java/java-stringbuffer.html
对字符串进行修改时使用
能够被多次的修改并且不产生新的未使用对象

# 数组

## 声明. 创建数组

1. dataType[] arrayRefVar = {value0, value1, ..., valuek}; 

2. dataType[] arrayRefVar = new dataType[arraySize];

## for each 循环遍历
for (double element: myList) {
   System.out.println(element);
}

# Scanner 

## 示例

通过创建Scanner类来获取用户的输入
通过next() nextLine() 接收字符串
通过 hasnext() hasNextLine() 判断是否有输入的数据

{% codeblock  %}
import java.util.Scanner; 
 
public class ScannerDemo {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        // 从键盘接收数据
 
        // next方式接收字符串
        System.out.println("next方式接收：");
        // 判断是否还有输入
        if (scan.hasNext()) {
            String str1 = scan.next();
            //String str2 = scan.nextLine();
            System.out.println("输入的数据为：" + str1);
        }
        scan.close();
    }
}
{% endcodeblock %}

## next() 与 nextLine() 区别
next():

1. 一定要读取到有效字符后才可以结束输入。
2. 对输入有效字符之前遇到的空白，next() 方法会自动将其去掉。
3只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符。
next() 不能得到带有空格的字符串。
nextLine()：

1. 以Enter为结束符,也就是说 nextLine()方法返回的是输入回车之前的所有字符。
2. 可以获得空白。

# 文件操作. 
{% post_link Java-io %}



# 异常处理
https://www.runoob.com/java/java-exceptions.html

## 遇到的报错记录

### The static field value.arr should be accessed in a static way

静态字段应以静态方式引用
接口中的变量前不需要加 this 
关键字 this 是java为了区分本类属性与外部的冲突而引入的一个调用方式，
这个 this 严格意义上讲，应当是调用本类引用属性或方法时使用的，而静态字段更多的是一个常驻与内存中的不变量，所以没必要使用 this 这个关键字

### Cannot make a static reference to the non-static method 

https://blog.csdn.net/weixin_43914658/article/details/109262885
main函数中只能调用静态函数，否则需要先实例化对象。

### java.lang.ArithmeticException: Non-terminating decimal expansion; no exact representable decimal result.

使用BigDecimal某些场景下对于如1/3会得到一个无穷小数，这个时候需要定义计算结果要保留到小数点后几位，否则就会抛出上面的异常。

public BigDecimal divide(BigDecimal divisor, int scale, int roundingMode)
BigDecimal b3 = b1.divide(b2, 4, BigDecimal.ROUND_HALF_UP);

<hr />

版权信息