<a name="gfeMi"></a>
## 常用类
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700569245403-dcaba375-7a56-4137-ac42-4bc657bc7a3e.png#averageHue=%23cbd8ad&clientId=u3c25ec9e-f549-4&from=paste&height=419&id=u022219f1&originHeight=833&originWidth=916&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=426888&status=done&style=none&taskId=uf0dd6cb6-4128-4d0c-93a0-be03185daa0&title=&width=460.79998779296875)
<a name="elLv7"></a>
### 基本数据类型的包装类 Wrapper Class
Java为了将基本数据类型与对象之间实现互相转化，为每一个基本数据类型都提供了相应的包装类。包装类位于java,lang包，八种包装类和基本数据类型的对应关系如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700569413717-b3031f49-0e32-4773-b549-b09943c29bcf.png#averageHue=%23f6d7bc&clientId=u3c25ec9e-f549-4&from=paste&height=286&id=ua0dd38ec&originHeight=916&originWidth=1296&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=440647&status=done&style=none&taskId=u8d212f3d-41c6-4cbb-889a-aad76693031&title=&width=404.4000244140625)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700569559280-b3f534ba-b783-4e92-a185-763322304529.png#averageHue=%23fcfcf7&clientId=u3c25ec9e-f549-4&from=paste&height=337&id=uf4e2304d&originHeight=853&originWidth=1620&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=525600&status=done&style=none&taskId=ufe42360a-e71a-4977-b6fe-e71e5a6747e&title=&width=639.4000244140625)<br />Number类是抽象类，它的所有子类都要提供实现这些抽象方法。包括intValue()、longValue()、flaotValue()、doubleValue()等，也就是说，所有的"数字型"包装类的类型可以互转。
```java
package com.nuobu;

// 测试包装类的使用
public class TestInteger {
    public static void main(String[] args) {
        // Integer i = new Integer(50); // 从java9开始被废弃
        Integer j = Integer.valueOf(10);

        int a = j.intValue(); // 把包装对象转为基本数据类型
        double b = j.doubleValue();

        Integer m = Integer.valueOf("456"); // 把字符串转化为数字

        System.out.println(Integer.MAX_VALUE); // 该类型的最大值范围
    }
}

```
<a name="yrXbR"></a>
### 自动装箱和拆箱
autoboxing and unboxing：将基本数据类型和包装类自动转换。
```java
// 自动装箱
Integer i = 100; // 编译器：Integer i = Integer.valueOf(100);
// 拆箱
int y = i; // 编译器：int y = i.intValue();

// Integer z = null;
// int z2 = z; // 会报空指针错误
```
自动装箱时，[-128,127]之间的数有缓存。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700571321264-ee06b8b5-040a-4d21-83b8-a8e4532f373f.png#averageHue=%23554537&clientId=u3c25ec9e-f549-4&from=paste&height=261&id=cMDaI&originHeight=326&originWidth=1512&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=431242&status=done&style=none&taskId=uf9d21c2b-4b2f-4e75-bb87-ddec61fe02f&title=&width=1209.6)
```java
Integer x1 = 100;
Integer x2 = 100;
Integer x3 = 1000;
Integer x4 = 1000;

System.out.println(x1 == x2); 
System.out.println(x3 == x4);
System.out.println(x1.equals(x2));
System.out.println(x3.equals(x4));

```
运行结果：<br />true<br />false<br />true<br />true
<a name="PFbwV"></a>
### String类
String类的对象是不可变的字符序列，StringBuilder和StringBuffer类对象字符序列可变。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700572456546-14b34717-e0ef-4dfd-bbc9-d62a1b6119dd.png#averageHue=%23e1d7d7&clientId=u3c25ec9e-f549-4&from=paste&height=93&id=uca681864&originHeight=392&originWidth=406&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=83097&status=done&style=none&taskId=udc157c15-f369-44aa-9703-988a0034364&title=&width=96.80001831054688)![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700572524243-6194c82d-c565-4cf0-8f87-3f7b7ccd9d79.png#averageHue=%23f4f1ed&clientId=u3c25ec9e-f549-4&from=paste&height=570&id=UWGFq&originHeight=712&originWidth=1787&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=719336&status=done&style=none&taskId=u57f79546-47bd-4fe0-98be-57d3dc68d9e&title=&width=1429.6)<br />编译器优化的问题：
```java
package com.nuobu;

public class TestString {
    public static void main(String[] args) {
        // 编译器做了优化，直接在编译的时候将字符串进行拼接
        String str1 = "hello" + " java"; // 相当于str1 = "hello java";
        String str2 = "hello java";
        System.out.println(str1 == str2); // true

        // 编译的时候不知道变量中存储的是什么，没法优化
        String str3 = "hello";
        String str4 = " java";
        String str5= str3 + str4;
        System.out.println(str2 == str5); // false
    }
}
```
<a name="LxNF2"></a>
### StringBuilder和StringBuffer类

- 可变字符序列。
- StringBuffer **线程安全（synchronized）**，做线程同步检查，但效率低。
- StringBuilder线程不安全，效率高。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700710375676-d7ee9fa5-ee10-4970-bd70-1e20fa9d9ae7.png#averageHue=%23f0efef&clientId=u1c73ecc9-66a2-4&from=paste&height=305&id=u117477c7&originHeight=381&originWidth=750&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=281745&status=done&style=none&taskId=u893235e9-34ab-494e-a4a0-e674ced0d2d&title=&width=600)
```java
// 测试StringBuilder和StringBuffer类
String str = "abc";
StringBuilder sb01 = new StringBuilder("abc");
StringBuffer sb02 = new StringBuffer("abc");

// StringBuilder
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 7; i++) {
    sb.append((char)('a'+i)); // 追加单个字符
}
System.out.println(sb.toString()); // 转换成String输出
sb.append(", I can sing my abc!"); // 追加字符串
System.out.println(sb.toString());

// StringBuffer,下面这些方法同样适用于StringBuilder
StringBuffer sb2 = new StringBuffer("王侯将相宁有种乎");
sb2.insert(0,"本").insert(0,"你说"); //插入字符串
System.out.println(sb2);
sb2.delete(0,2);  // 删除子字符串
System.out.println(sb2);
sb.deleteCharAt(0).deleteCharAt(0); // 删除某个字符
System.out.println(sb2.charAt(0)); // 获取某个字符
System.out.println(sb2.reverse()); // 字符串逆序
```
运行结果：<br />abcdefg<br />abcdefg, I can sing my abc!<br />你说本王侯将相宁有种乎<br />本王侯将相宁有种乎<br />本<br />乎种有宁相将侯王本

- **使用字符串进行拼接时需要注意的问题**
```java
package com.nuobu;

public class TestString2 {
    public static void main(String[] args) {
        // 使用String字符串进行拼接
        String str8 = "";

        long num1 = Runtime.getRuntime().freeMemory(); // 获取系统剩余内存空间
        long time1 = System.currentTimeMillis(); // 获取系统当前时间
        for (int i = 0; i < 5000; i++) {
            str8 = str8 + i; // 相当于产生了5000个对象
        }
        long num2 = Runtime.getRuntime().freeMemory(); // 获取系统剩余内存空间
        long time2 = System.currentTimeMillis(); // 获取系统当前时间
        System.out.println("String占用内存：" + (num1 - num2));
        System.out.println("String占用时间：" + (time2 - time1));

        // 使用StringBuilder字符串进行拼接
        StringBuilder sb1 = new StringBuilder("");
        long num3 = Runtime.getRuntime().freeMemory(); // 获取系统剩余内存空间
        long time3 = System.currentTimeMillis(); // 获取系统当前时间
        for (int i = 0; i < 5000; i++) {
            sb1.append(i);
        }
        long num4 = Runtime.getRuntime().freeMemory(); // 获取系统剩余内存空间
        long time4 = System.currentTimeMillis(); // 获取系统当前时间
        System.out.println("StringBuilder占用内存：" + (num3 - num4));
        System.out.println("StringBuilder占用时间：" + (time4 - time3));
    }
}

```
运行结果：<br />String占用内存：21591456<br />String占用时间：20<br />StringBuilder占用内存：0<br />StringBuilder占用时间：0<br />**字符串拼接时，使用StringBuilder代替！！不要使用String。**
<a name="F6qOl"></a>
### 时间处理相关类
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700711519619-682fed85-302f-4ff7-9c90-2bf77d257a99.png#averageHue=%23f1f0ef&clientId=u1c73ecc9-66a2-4&from=paste&height=792&id=uacc71c08&originHeight=990&originWidth=2125&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1234776&status=done&style=none&taskId=ucf7933f4-1577-4928-94bd-0851e82c259&title=&width=1700)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700711580791-43ceb9d7-cf6c-41d1-a8ff-2d38e7bedcab.png#averageHue=%23f7f4ef&clientId=u1c73ecc9-66a2-4&from=paste&height=438&id=u8a60ce38&originHeight=547&originWidth=2055&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=466632&status=done&style=none&taskId=u676e3a45-39d7-49cb-be82-e736c19cf8b&title=&width=1644)
<a name="Rnhno"></a>
#### 时间类 Date
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700711694418-dd531b5e-ff61-4bc1-aae5-b991aba084c0.png#averageHue=%23f1f0f0&clientId=u1c73ecc9-66a2-4&from=paste&height=897&id=u5dde1a68&originHeight=1121&originWidth=2104&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1301892&status=done&style=none&taskId=u3462d8ce-d3a9-4a2a-bdf1-8b4afc5bee2&title=&width=1683.2)
```java
package com.nuobu;

import java.util.Date;

// 测试时间类
public class TestDate {
    public static void main(String[] args) {
        long nowNum = System.currentTimeMillis(); // 当前毫秒数
        System.out.println(nowNum);

        Date date1 = new Date();  // 无参，当前时间
        System.out.println(date1);
        Date date2 = new Date(10000000002032L);
        System.out.println(date2);
        Date date3 = new Date(-21L*365*24*3600*1000); // 1970-1949
        System.out.println(date3);
    }

}
```
<a name="Y1GW6"></a>
#### 时间格式化类 DateFormat/SimpleDateFormat
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700712298613-be3378c4-4a6a-4e97-a854-67585b5af07f.png#averageHue=%23ebebea&clientId=u1c73ecc9-66a2-4&from=paste&height=228&id=u775d88d8&originHeight=285&originWidth=1988&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=447861&status=done&style=none&taskId=u6eae63de-816a-4b70-a90e-7f2484eb7c6&title=&width=1590.4)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700712941472-568a5d61-865b-4733-a560-e1c52827594a.png#averageHue=%23f5f5f4&clientId=u1c73ecc9-66a2-4&from=paste&height=765&id=udc4795a6&originHeight=956&originWidth=2138&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=729838&status=done&style=none&taskId=u4e23fe41-4d7d-4688-9b90-fe9c0d79fc5&title=&width=1710.4)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700713024207-8a220d5f-521b-436d-aea5-674277819a21.png#averageHue=%23f5f5f5&clientId=u1c73ecc9-66a2-4&from=paste&height=642&id=u53731089&originHeight=802&originWidth=2135&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=698352&status=done&style=none&taskId=uef331575-7200-4463-87c7-c4a0936b7a1&title=&width=1708)
```java
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class TestDateFormat {
    public static void main(String[] args) throws ParseException {
        DateFormat format = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
        String str = "2049-10-1 10:10:10";

        Date guoqing100 = format.parse(str);
        System.out.println(guoqing100.getTime());
        System.out.println(guoqing100);

        DateFormat format1 = new SimpleDateFormat("yyyy年MM月dd日 hh时");
        Date date2 = new Date();
        String date2Str = format1.format(date2);
        System.out.println(date2Str);

        // 一些用法
        Date now = new Date();
        DateFormat f1 = new SimpleDateFormat("今天是今年的第D天,是本月的第d天，是本星期的E");
        String nowD = f1.format(now);
        System.out.println(nowD);
        DateFormat f2 = new SimpleDateFormat("本周是今年的w周,是本月的第W周");
        String nowW = f2.format(now);
        System.out.println(nowW);
        DateFormat f3 = new SimpleDateFormat("今天是yyyy年的第D天,是MM月的第d天，是w周的E");
        String guoqing100Str = f3.format(guoqing100);
        System.out.println(guoqing100Str);
    }
}

```
运行结果：<br />2516667010000<br />Fri Oct 01 10:10:10 CST 2049<br />2023年11月23日 12时<br />今天是今年的第327天,是本月的第23天，是本星期的周四<br />本周是今年的48周,是本月的第4周<br />今天是2049年的第274天,是10月的第1天，是40周的周五
<a name="Tjqkl"></a>
#### 日历类 Calendar/GregorianCalendar
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700713754251-d313c329-e162-4b3d-b488-f3807c76d421.png#averageHue=%23f9f5f5&clientId=u1c73ecc9-66a2-4&from=paste&height=826&id=ud9a9af37&originHeight=1033&originWidth=2082&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=675798&status=done&style=none&taskId=u6e60e367-2b0f-49dd-b3d9-4cacd37001b&title=&width=1665.6)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700713840396-d78297e0-bc60-49be-bda1-7a40254f8da7.png#averageHue=%23c8c4be&clientId=u1c73ecc9-66a2-4&from=paste&height=287&id=u1c3756e6&originHeight=359&originWidth=2137&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=681746&status=done&style=none&taskId=u36770431-9176-4381-82cc-c4a57c05c14&title=&width=1709.6)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700713963815-2515c9d6-e6c9-4edb-8d08-668fa0fa2c9d.png#averageHue=%23443f38&clientId=u1c73ecc9-66a2-4&from=paste&height=556&id=u999bdf5d&originHeight=695&originWidth=2024&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1141157&status=done&style=none&taskId=u534cfdec-d31f-4e21-8986-76024147c53&title=&width=1619.2)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700714014045-d7ac5e45-def9-4039-8fca-f119d8e63fd8.png#averageHue=%23484137&clientId=u1c73ecc9-66a2-4&from=paste&height=654&id=ue774ed6e&originHeight=818&originWidth=1856&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1303848&status=done&style=none&taskId=ua1967ec7-0f59-4a17-ba61-5082a1c9ba1&title=&width=1484.8)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700714400070-98018c4f-ac0a-4494-aa23-070e0807888b.png#averageHue=%232e2e2d&clientId=u1c73ecc9-66a2-4&from=paste&height=222&id=u0c5afe40&originHeight=278&originWidth=1899&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=359661&status=done&style=none&taskId=ubb8dea44-098f-4ee9-8f14-32742a89b61&title=&width=1519.2)
<a name="ZoGtl"></a>
### Math类和Random类
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700721397099-5b4b5e62-706b-4935-b0a5-9b9d5f36a6d2.png#averageHue=%23f4f4f3&clientId=u1c73ecc9-66a2-4&from=paste&height=924&id=u592efc3b&originHeight=1155&originWidth=1902&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1243815&status=done&style=none&taskId=u1a76539d-8929-47cf-a206-fbf1777f97e&title=&width=1521.6)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700721660591-4443c328-28aa-48c0-b46e-e868121049f7.png#averageHue=%232f2d2b&clientId=u1c73ecc9-66a2-4&from=paste&height=226&id=u7e469ccb&originHeight=283&originWidth=1575&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=321631&status=done&style=none&taskId=ubf7ff0a2-b076-4ad0-809d-be0d72fe49e&title=&width=1260)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700721603349-0b4de10a-7acb-4d9d-86ee-33a16925be18.png#averageHue=%2342403c&clientId=u1c73ecc9-66a2-4&from=paste&height=766&id=u45b2761f&originHeight=958&originWidth=1413&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1386542&status=done&style=none&taskId=ubbadb5e4-5445-446e-a774-f0472fcbbee&title=&width=1130.4)
<a name="Jlldb"></a>
### File类
java.io.File类：读取、创建、删除、修改文件。
```java
package com.nuobu;

import java.io.File;
import java.io.IOException;

public class TestFile1 {
    public static void main(String[] args) throws IOException {
        System.out.println(System.getProperty("user.dir"));
        File f = new File("a.txt"); // 相对路径：默认放到user.dir目录下
        f.createNewFile(); // 创建文件
        File f2 = new File("F:/Code/Java/Mycode/demo/b.txt"); // 绝对路径
        f2.createNewFile();
    }
}

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700722331036-c63bf841-7e20-447a-940f-6505f67485dc.png#averageHue=%23f0d8c2&clientId=u1c73ecc9-66a2-4&from=paste&height=739&id=u8f6826dd&originHeight=924&originWidth=1646&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=954917&status=done&style=none&taskId=u7093b17b-6203-484f-b25f-28177cb8ead&title=&width=1316.8)
```java
System.out.println("File是否存在："+f.exists());
System.out.println("File是否是目录："+f.isDirectory());
System.out.println("File是否是文件："+f.isFile());
System.out.println("File最后修改时间："+new Date(f.lastModified()));
System.out.println("File的大小："+f.length());
System.out.println("File文件名："+f.getName());
System.out.println("File的目录相对路径："+f.getPath());
System.out.println("File的目录绝对路径："+f.getAbsoluteFile());
```
运行结果：<br />File是否存在：true<br />File是否是目录：false<br />File是否是文件：true<br />File最后修改时间：Thu Nov 23 14:49:29 CST 2023<br />File的大小：0<br />File文件名：a.txt<br />File的目录相对路径：a.txt<br />File的目录绝对路径：F:\Code\Java\Mycode\demo\a.txt

创建目录：<br />mkdir mkdirs
```java
File f3 = new File("d:/电影/华语/大陆");
// boolean flag = f3.mkdir(); // 目录结构中有一个不存在，就不会创建目录树，创建失败
f3.mkdirs(); // 成功在d盘中创建电影、华语、大陆三级目录
```

递归打印目录结构：
```java
package com.nuobu;

import java.io.File;

public class PrintFileTree {
    public static void main(String[] args) {
        System.out.println(System.getProperty("user.dir"));
        File f = new File(System.getProperty("user.dir"));
        printFile(f,0);
    }

    static void printFile(File file, int level){
        for (int i = 0; i < level; i++) {
            System.out.print("-");
        }
        // 输出文件名
        System.out.println(file.getName());

        if(file.isDirectory()){
            File[] files = file.listFiles(); // 列出所有子文件、子目录
            for (File temp:files) {
                printFile(temp,level+1);
            }
        }
    }
}
```
<a name="SNOqe"></a>
### 枚举
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700723663101-0b275a82-b67b-45e7-b080-5deb345f8dd6.png#averageHue=%23f4f3f3&clientId=u1c73ecc9-66a2-4&from=paste&height=302&id=u040699f3&originHeight=378&originWidth=1799&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=294492&status=done&style=none&taskId=ud9da1a42-e171-45c7-8299-f5ff75575f5&title=&width=1439.2)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700723717829-2564f69d-127a-4e9c-bf63-bea9343cb6c3.png#averageHue=%23f2f1f1&clientId=u1c73ecc9-66a2-4&from=paste&height=499&id=udc90dc21&originHeight=624&originWidth=2042&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=703584&status=done&style=none&taskId=ud4759064-42c1-4219-a827-d765e6530b7&title=&width=1633.6)
```java
package com.nuobu;

import java.util.Random;

// 测试枚举
public class TestEnum {
    public static void main(String[] args) {
        System.out.println(Jijie.AUTUMN);
        System.out.println(Season.AUTUMN); // 枚举

        for(Season s:Season.values()){
            System.out.println(s);
        }

        int a = new Random().nextInt(4); // 生成0，1，2，3随机数
        switch (Season.values()[a]){
            case SPRING:
                System.out.println("春天");
                break;
            case SUMMER:
                System.out.println("夏天");
                break;
            case AUTUMN:
                System.out.println("秋天");
                break;
            case WINTER:
                System.out.println("冬天");
                break;
        }
    }
}

enum Season {
    SPRING,SUMMER,AUTUMN,WINTER
}

class Jijie{
    public static final int SPRING = 0;
    public static final int SUMMER = 0;
    public static final int AUTUMN = 0;
    public static final int WINTER = 0;
}

```
运行结果：<br />0<br />AUTUMN<br />SPRING<br />SUMMER<br />AUTUMN<br />WINTER<br />冬天

<a name="IVkff"></a>
## 异常
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700728550389-6d67d464-8b8f-4fbc-887d-66497480855e.png#averageHue=%23c4f096&clientId=u1c73ecc9-66a2-4&from=paste&height=612&id=ua053d242&originHeight=765&originWidth=1799&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=625192&status=done&style=none&taskId=u9805f38c-624b-42e7-9b79-da7254681ff&title=&width=1439.2)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700729246014-1cc4b286-5479-418e-afed-a6bff558b8d5.png#averageHue=%23d5d2cb&clientId=u1c73ecc9-66a2-4&from=paste&height=404&id=s6x9q&originHeight=505&originWidth=1956&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=917318&status=done&style=none&taskId=u472a31f1-4004-4e63-a707-8a40b185e57&title=&width=1564.8)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700729375928-39cd4ba1-7f27-4ecc-bb2b-1bc03fb4d444.png#averageHue=%23f4f4f3&clientId=u1c73ecc9-66a2-4&from=paste&height=340&id=u1eddd566&originHeight=425&originWidth=1942&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=500558&status=done&style=none&taskId=u7cb2fea8-7b43-4d38-a7d7-e92163d686c&title=&width=1553.6)
<a name="T2lb5"></a>
### 异常机制 Exception
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700728878912-a2f03a30-d407-45cb-944b-76949ad9116d.png#averageHue=%23d4d1ca&clientId=u1c73ecc9-66a2-4&from=paste&height=258&id=ub03869c9&originHeight=323&originWidth=1959&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=602499&status=done&style=none&taskId=u9fa05cd8-c96f-4dc9-9a0c-5c0ecf35f5a&title=&width=1567.2)
```java
package com.nuobu;

public class Test01 {
    public static void main(String[] args) {
        System.out.println("11111111");
        try{
            int a = 1/0;
        }catch (Exception e){
            e.printStackTrace();
        }
        System.out.println("22222222222");
    }
}
```
运行结果：<br />11111111<br />22222222222<br />java.lang.ArithmeticException: / by zero<br />	at com.nuobu.Test01.main(Test01.java:7)
<a name="wGzuu"></a>
### 异常处理
<a name="faNNi"></a>
#### （1）逻辑上避免
```java
// 除0
b = 0;
if(b != 0){
    a = 20/b;
}

// 空指针异常
str = null;
if(str != null){
    System.out.println(str.charAt(0));
}

// 类型转化异常
Animal a = new Cat();
if (a instanceof Dog){
    Dog d = (Dog) a;
}

 // 数组越界
int [] arr = new int[5];
int index = 5;
if (index>0 && index < arr.length){
    System.out.println(arr[index]);
}

 // 字符串转数字
import java.util.regex.Matcher;
import java.util.regex.Pattern;
String str = "1234aass";
Pattern p = Pattern.compile("^\\d+$");
Matcher m = p.matcher(str);
if(m.matches()){ // 如果str匹配代表数字的正则表达式，才会转换
    System.out.println(Integer.parseInt(str));
}

```

<a name="VFZ8k"></a>
#### （2）异常捕获 try-catch-finally
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700730406573-64e6ab8a-f06d-46b3-bc67-345f28519a38.png#averageHue=%23c2ef92&clientId=u1c73ecc9-66a2-4&from=paste&height=280&id=ua40c6e62&originHeight=939&originWidth=1456&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=916268&status=done&style=none&taskId=uc5996ae1-ebed-4553-a611-0cc6bdb0658&title=&width=434)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700730618499-9daaa65c-fe55-4a74-98e3-ed2cfa0fa772.png#averageHue=%23e4e3e3&clientId=u1c73ecc9-66a2-4&from=paste&height=152&id=u08165403&originHeight=190&originWidth=1912&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=265354&status=done&style=none&taskId=uae9c583e-ed00-4f70-b7b0-511915d15d8&title=&width=1529.6)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700730698118-39ff1382-2d1c-44a8-b12b-14e07651dde4.png#averageHue=%23f0f0f0&clientId=u1c73ecc9-66a2-4&from=paste&height=539&id=u4f9d9f66&originHeight=674&originWidth=1939&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=800205&status=done&style=none&taskId=u7f570ad2-b3f7-43c4-9759-2b4013950e5&title=&width=1551.2)
```java
package com.nuobu;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class Test02 {
    public static void main(String[] args) {
        FileReader reader = null;
        try {
            reader = new FileReader(System.getProperty("user.dir") +"/a.txt");
            char c = (char)reader.read();
            char c2 = (char)reader.read();
            System.out.println(""+c+c2);
        } catch (FileNotFoundException e) {
            throw new RuntimeException(e);
        } catch (IOException e) {
            throw new RuntimeException(e);
        } finally {
            try {
                if(reader != null){
                    reader.close();
                }
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }
    }
}

```
<a name="ROKl3"></a>
#### （3）声明异常（throws子句）
```java
package com.nuobu;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class Test03 {
    public static void main(String[] args) throws IOException {
        FileReader reader = null;
        try {
            reader = new FileReader(System.getProperty("user.dir") +"/a.txt");
            char c = (char)reader.read();
            char c2 = (char)reader.read();
            System.out.println(""+c+c2);
        } finally {
            try {
                if(reader != null){
                    reader.close();
                }
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }
    }
}

```
**关闭资源的另一种实现方式：try-with-resource**。自动关闭实现了AutoCloseable接口的类。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700732103658-d7f004bd-b86f-432c-8b2f-502d96ef45c0.png#averageHue=%23f1f0f0&clientId=u1c73ecc9-66a2-4&from=paste&height=713&id=ua9fc79bb&originHeight=891&originWidth=2052&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1602805&status=done&style=none&taskId=ue9db0f6c-513b-4cf6-b33c-c0df1919356&title=&width=1641.6)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700731965353-c9fce121-9472-4b08-9787-135a0b3a061f.png#averageHue=%23fdf9f9&clientId=u1c73ecc9-66a2-4&from=paste&height=394&id=udb20d107&originHeight=492&originWidth=1552&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=107395&status=done&style=none&taskId=ub1e0fc32-ae45-48bf-9c7f-6f6294fe41c&title=&width=1241.6)
```java
package com.nuobu;

import java.io.FileReader;

public class Test04 {
    public static void main(String[] args) {
        try(FileReader reader = new FileReader(System.getProperty("user.dir") +"/a.txt");){
            char c = (char)reader.read();
            char c2 = (char)reader.read();
            System.out.println(""+c+c2);
        }catch (Exception e){
            e.printStackTrace();
        }
    }
}

```
try括号中打开的资源都能自动关闭，不需要写finally块来执行reader.close()，世界都变得美好了！！！
<a name="Nzaox"></a>
### 自定义异常
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700732581164-273b95a2-fe64-49e6-916c-f1d2109eaac3.png#averageHue=%23d6d4ce&clientId=u1c73ecc9-66a2-4&from=paste&height=538&id=uedc48955&originHeight=672&originWidth=1932&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1184965&status=done&style=none&taskId=u629a8f19-1ce9-4a2d-83e4-397490f7ff4&title=&width=1545.6)
```java
package com.nuobu;

// 年龄非法异常
public class IllegalAgeException extends Exception{
    // 默认构造器
    public IllegalAgeException(){}
    // 带详细信息的构造器，信息存储在message中
    public IllegalAgeException(String message){super(message);}
}
```
```java
package com.nuobu;

public class TestMyException {
    public static void main(String[] args) throws IllegalAgeException {
        Person p = new Person();
        p.setAge(-1);
    }
}

class Person{
    private String name;
    private int age;

    public void setName(String name) {this.name = name;}
    public void setAge(int age) throws IllegalAgeException {
        if (age < 0){
            throw new IllegalAgeException("人的年龄不应该为负数！");
        }
        this.age = age;
    }

    public String toString() {return "name is " + name +", age is " + age;}
}

```
运行结果：<br />Exception in thread "main" com.nuobu.IllegalAgeException: 人的年龄不应该为负数！<br />	at com.nuobu.Person.setAge(TestMyException.java:21)<br />	at com.nuobu.TestMyException.main(TestMyException.java:6)


