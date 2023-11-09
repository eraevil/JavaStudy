## Java基础
1. Java对大小写敏感。
2. 关键字class的意思是类。java是面向对象的语言，所有代码必须位于类里面。
3. 源文件编译后，得到相应的字节码文件，编译器为每个类生成独立的字节码文件。
4. main方法是java应用程序的入口方法，格式固定：
```java
public static void main(String[] args) {...}
```

5. 一个源文件可以包含多个类。
6. 每个语句必须以分号结束，回车不是语句的结束标志，所以一个语句可以跨多行。
7. Java编译时会跳过注释语句。**多行注释不支持嵌套使用。**
```java
//单行注释

/* 
多行注释
*/

/**
文档注释
@author nuobu
*/
```
<br />
## 变量

1. 标识符规则：

1）必须以字母、下划线_、美元符$开头。<br />2）其他部分可以是字母、下划线_、美元符$和数字的任意组合（**数字不可以开头**）。<br />3）大小写敏感，且长度无限制。<br />4）**不可以是Java关键字。**<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698651300762-acbf2ba2-4a80-4c08-9ed3-5116f539c7de.png#averageHue=%23efefef&clientId=u91c1dfc5-bc9b-4&from=paste&height=229&id=u7abdb3be&originHeight=883&originWidth=1534&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=507400&status=done&style=none&taskId=u2ddef919-3f09-4158-aeb1-8bb5adb349e&title=&width=397.66668701171875)

2. 命名尽量使用驼峰法。变量、方法、类名见名知义。
3. Java不采用ASCII字符集，而采用Unicode字符集，因此字母可以是汉字，**但不建议使用汉字作为标识符**。
4. Java是强类型语言，每个变量必须声明其数据类型。**变量要使用必须先声明。**变量类型决定了空间的大小。

int 4 字节  <br />double 8 字节 <br />long 8 字节

5. 变量分类和作用域：局部变量、成员变量和静态变量。

**局部变量**：属于方法或代码块。从声明位置开始，到方法或语句块执行完毕，杀掉。<br />成员变量：属于对象。对象创建，则成员变量创建，对象消失则一同消失。<br />静态变量：属于类。用static修饰，类被加载，静态变量就有效，类被卸载，静态变量消失。

6. **常量**：一生只爱一个人，一生只赋一次值。
```java
final int NUM= 12;
```
常量的命名：全用大写字母，单词之间用下划线隔开。
## 数据类型
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698652794156-b38f7377-31f7-4bd3-9a27-9ebe16b73319.png#averageHue=%23fdfdfb&clientId=u91c1dfc5-bc9b-4&from=paste&height=390&id=u4d56e6c1&originHeight=733&originWidth=1374&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=260089&status=done&style=none&taskId=ue1a98061-0d58-4845-96c1-9fbd583cd73&title=&width=731.6666870117188)
### 整型
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698653019841-1ea5d10e-601d-4856-a093-d8be52f1b169.png#averageHue=%23c7d7a2&clientId=u91c1dfc5-bc9b-4&from=paste&height=138&id=u337f1d1f&originHeight=298&originWidth=1509&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=238860&status=done&style=none&taskId=u9c28eac7-850c-4356-b4fc-564e985374d&title=&width=698.7802734375)<br />十进制，如99，-200<br />八进制，以0开头，如015<br />十六进制，以0x或0X开头，如0x15<br />二进制，以0b或0B开头，如0b01110011<br />整型默认是int，定义长整型：long a = 10000000000L;
### 浮点型
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698653787831-4675b4e4-8dee-4ad3-a3b5-3e56c7c6c701.png#averageHue=%23bfd295&clientId=u91c1dfc5-bc9b-4&from=paste&height=85&id=u2a91c005&originHeight=183&originWidth=1510&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=144610&status=done&style=none&taskId=u815ebbad-0255-4075-bc00-11987eb4e63&title=&width=703.7802734375)<br />单精度float，双精度double，绝大部分程序采用双精度类型。<br />**浮点型不精确**，不用于比较。指不适合精度要求很高的商业计算，需要要使用BigDecimal进行运算和比较。
```java
float f2 = 0.1f;
double d3 = 1.0/10;
System.out.println(f2==d3); // false
float f4 = 234335452662L;
float f5 = f4 + 1;
System.out.println(f4==f5); // true
```
浮点常量默认类型为double，要改成float可以后加F或f。
### 字符型 char 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698654550666-83f4182b-621c-47d6-a28e-8c2a793fb456.png#averageHue=%23faf8f8&clientId=u91c1dfc5-bc9b-4&from=paste&height=257&id=uc96e92f2&originHeight=609&originWidth=1071&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=213421&status=done&style=none&taskId=u7043d9b3-1873-445e-85f2-851465f917c&title=&width=452.085205078125)![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698654583242-dd56c59d-86d1-4f37-ae57-b09e3fa5377a.png#averageHue=%23cedee8&clientId=u91c1dfc5-bc9b-4&from=paste&height=286&id=u91f4bd55&originHeight=718&originWidth=606&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=801558&status=done&style=none&taskId=u2b881713-8257-4eaf-96df-2c39377507a&title=&width=241.2518768310547)<br />Java中字符采用Unicode编码，支持65536个字符的表示。<br />Java中字符串不是基本数据类型。<br />可使用转义字符: \n \' \"避免引起歧义。
### 布尔型 boolean
 boolean类型有true和false两个常量值。<br />在内存中占1个字节或4个字节，不可以使用0或非0的整数来替代true和false。
```java
// 布尔型
boolean b1 = 1;
boolean b2 = false;
if(b1){
    System.out.println("b1 is true");
}else{
    System.out.println("b1 is false");
}
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698667829475-7a00f528-a8c9-4ef2-b1f6-b8b71a925d1d.png#averageHue=%23171717&clientId=u91c1dfc5-bc9b-4&from=paste&height=153&id=YiNrl&originHeight=337&originWidth=790&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=32195&status=done&style=none&taskId=u77fd8b21-d659-4f21-8b27-56df3b796e3&title=&width=359.787841796875)
## 运算符
 ![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698667941487-a4d99970-9dbe-44a6-b321-56b5bf6e61df.png#averageHue=%23b3d19e&clientId=u91c1dfc5-bc9b-4&from=paste&height=248&id=ue11518e7&originHeight=508&originWidth=1433&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=308234&status=done&style=none&taskId=u1386b21f-2662-40e3-aad8-b692588e907&title=&width=698.7802734375)
### 算术运算符

- 整数运算

如果两个操作数有一个为long，则结果也为long。
```java
long a = 3;
int b = 4;
int c = a+b;
System.out.println(c);
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698669315120-0f765861-f40e-45df-9726-ff804d2cc24e.png#averageHue=%23191919&clientId=u91c1dfc5-bc9b-4&from=paste&height=96&id=u041b10d6&originHeight=159&originWidth=801&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=17355&status=done&style=none&taskId=ua4703c30-2056-4792-bb8d-14137373e23&title=&width=485.45451739603)<br />没有long时，结果为int。即使操作数全为short，byte，结果也是int。<br />两个整数相除，直接保留整数部分，没有四舍五入。
```java
int d2 = 32/3; // 10
```

- 浮点运算

如果两个操作数有一个为double，则结果也为double。<br />只有两个操作数都为float，结果才是float。

- 取模运算

其操作数可以为浮点数，一般使用整数，结果是“余数”，“余数”符号和左边操作数相同，如：7%3 = 1，-7%3 = -1，7%-3 = 1。
### 赋值运算符和扩展运算符
     ![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698669740779-b7c6a366-f5a2-49dd-aa4b-ef86e8ed6648.png#averageHue=%23c8d9a5&clientId=u91c1dfc5-bc9b-4&from=paste&height=216&id=Yr5wq&originHeight=357&originWidth=1186&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=163886&status=done&style=none&taskId=ue5a46ccc-2278-4c5b-9251-b3e49050353&title=&width=718.7878372430606)
### 关系运算符
运算结果为boolean值。<br />=是赋值运算符，==是关系运算符。<br />==、!=所有数据类型都可以使用，包括基本数据类型和引用数据类型。<br />>、<、>=、<=仅针对数值类型以及char。**char值位于0~65536之间，可以通过(int)强制转型成数字。**
### **逻辑运算符**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698670477648-7ba57840-c5dd-4457-a773-0660e19a6697.png#averageHue=%23c8d8a5&clientId=u91c1dfc5-bc9b-4&from=paste&height=253&id=u31eed449&originHeight=418&originWidth=1275&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=208112&status=done&style=none&taskId=u50bb6071-050d-4fff-8663-8c276d87a07&title=&width=772.7272280648417)<br />&&、|| 采用短路的方式。**从左到右计算，如果左边就能判断真假，就不会计算右边的运算。**
### **位运算符**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698670924602-a2c3be5e-383d-4d14-a96b-2665c745ce18.png#averageHue=%23c8d8a6&clientId=u91c1dfc5-bc9b-4&from=paste&height=251&id=ucdac856e&originHeight=414&originWidth=1278&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=199054&status=done&style=none&taskId=u97de7f70-d1f4-46b7-b52f-a662ed529ef&title=&width=774.5454097779354)
```java
int a = 7; // 0000 0111
int b = 8; // 0000 1000
System.out.println(a&b); // 0000 0000 0
System.out.println(a|b); // 0000 1111 15
System.out.println(a^b); // 0000 1111 15
System.out.println(~b); // 1111 0111 -9

// 移位
int c = 5<<1; // 相当于：5*2
System.out.println(c); // 10 
int d = 5<<2; // 相当于：5*2*2
System.out.println(d); // 20
int e = 40>>3;// 相当于：40/8
System.out.println(e); // 5
```
### **字符串连接符**
+两个操作算子有一个为字符串则为连接符，转化为字符串。**注意！是String不是char！**
### 条件运算符
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698905706539-f8da10da-f825-4b47-b91c-fbe0cc7295e9.png#averageHue=%23dad69d&clientId=uad6b452f-2d10-4&from=paste&height=166&id=u5aca0298&originHeight=274&originWidth=667&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=65357&status=done&style=none&taskId=u6fb1444b-8e05-475a-939f-cb5867675ab&title=&width=404.2424008778427)
### 运算符优先级
括号运算符 > 一元运算符(!、正负号) > 位逻辑运算符 >自增自减 > 算数运算符（乘除模、加减） > 关系运算符 > 位运算符 > 条件运算符 > 扩展运算符<br />**逻辑非 > 逻辑与 > 逻辑或**
```java
boolean s1=true,s2=true,s3=false;
System.out.println(s1||s2&&s3); // true 先执行s2&&s3,再执行s1||true
```

## 数据类型转换

1. 容量小的数据类型可以**自动转换**为容量大的数据类型。这个过程可能会造成精度的损失。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698910196601-af0c3b0b-c0bd-4c7d-b813-73cca39a557f.png#averageHue=%23f7f5f5&clientId=uad6b452f-2d10-4&from=paste&height=196&id=u22361633&originHeight=323&originWidth=650&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=100113&status=done&style=none&taskId=u7726de30-88de-4ffd-85b8-c340009da04&title=&width=393.93937117031146)<br />**特例**：整型常量是int类型，但是可以自动转换成：byte/short/char。<br />只要不超过该类型表示的范围。
```java
int a = 2345;
long b = a;
//int c = b; // long类型不能转换为int
double d = b;
float f = b;
// 特例：整型常量是int类型，但是可以自动转换成：byte/short/char
// 只要不超过该类型表示的范围
byte h1 = 123;
// byte h2 = 1234; // 报错
char h3 = 97;
```

2. **强制类型转换**（cast）。用于强制转换数值的类型，可能损失精度。
```java
double a = 3.94152;
int b = (int)a; // 结果：3。浮点数强制转整数，直接丢失小数部分。
System.out.println(b);

int c = 97;
char d = (char)c;
System.out.println(d); // a

// 强制转型，超过了表数的范围，则会转成一个完全不同的值。
byte e = (byte)300;
System.out.println(e); // 44
```

3. 基本类型转化时常见的错误和问题。
   - 操作比较大的数时，要留意是否溢出，尤其是操作整数时。
```java
int money = 1000000000; // 10亿
int years = 20;
int total = money*years;
System.out.println(total); // -1474836480 溢出
long total1 = money*years;
System.out.println(total1); // -1474836480 计算money*years时已经溢出，结果仍是一个溢出的int，赋给long类型，仍然是一个溢出的负数
long total2 = money*((long)years);
System.out.println(total2); // 20000000000
```

   - 不要命名名字为l的变量，容易与1混淆。
   - long类型使用大写L，不要使用小写l。
## 控制语句
顺序结构、条件判断结构、循环结构

1. 条件判断结构

![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698918963351-cbf03a4d-ebd8-4277-a0ea-da5352db14a4.png#averageHue=%23ebe7e3&clientId=uab043a09-b24c-4&from=paste&height=163&id=u1088df07&originHeight=269&originWidth=731&originalType=binary&ratio=1.100000023841858&rotation=0&showTitle=false&size=96425&status=done&style=none&taskId=u402597fd-0983-4a04-b148-5f8888b1d28&title=&width=443.0302774238426)

2. 循环结构

当型：while、for<br />直到型：do-while<br />嵌套循环、break、continue<br />**Tips: **带标签的continue，很特殊的一种"label:/goto"的用法。**帮助我们从内部循环跳到外部循环。**
```java
outer:for (int i = 101; i < 150; i++){
    for (int j = 2; j < i / 2; j++) {
        if (i % j== 0) continue outer; //符合某条件，跳到外部循环继续
    }
    System.out.print(i + " ");
}
System.out.println("");
```
## 函数
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1698933004513-b02fc5c5-4d5e-4fb8-a9cb-0b405e06d9aa.png#averageHue=%23fbfaf4&clientId=uab043a09-b24c-4&from=paste&height=442&id=ue6f6ddb7&originHeight=730&originWidth=1289&originalType=binary&ratio=1.100000023841858&rotation=0&showTitle=false&size=281583&status=done&style=none&taskId=u8b816e7c-3494-45e2-8ef6-c565189d48c&title=&width=781.2120760592792)

1. 方法的重载overload

一个类中可以定义多个名称相同，单参数列表不同的方法。<br />**构成函数重载的条件**：

   - 不同含义：形参类型、形参个数、形参顺序
   - 只有返回值不同不构成方法的重载。如int a(String str){} 和 void a(String str){}。
   - 只有形参名称不同，不构成方法的重载。如int a(String str){} 和 int a(String s){}。
2. 递归函数：自己调用自己的函数。算法简单，但是调用过程中会占用大量系统栈，内存消耗过多，在递归调用层次多的时速度比循环要慢得多，谨慎使用。
# 



