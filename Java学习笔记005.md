<a name="gfeMi"></a>
## 数组
<a name="elLv7"></a>
### 基本概念
数组是相同类型数据的有序结合。其中，每一个数据称为一个元素，每个元素通过索引访问。有以下基本特点：

- 长度是确定的。数组一旦被创建，它的大小就是不可改变的。
- 其元素类型必须相同，不能出现混合类型。
- 数组类型可以是任何数据类型，包括基本类型和引用类型。
- 数组变量属于引用类型，数组也是对象，数组中的元素相当于对象的属性。
```java
// 数组声明方式
type [] arr_name;  // 方式一
type arr_name[]; // 方式二
```

- 声明的时候并没有实例化任何对象，只有在实例化数组的时候，JVM才分配空间，此时才与长度有关。
- 声明一个数组时，数组并没有被真正创建。
- 构造一个数组，必须指定长度。
```java
package com.nuobu;

// 数组的声明和创建
public class Test01 {
    public static void main(String[] args) {
        int[] s; // 声明数组
        s = new int[10]; // 给数组分配空间
        for (int i = 0; i < 10; i++){
            s[i] = 2 * i +1; // 给数组元素赋值，数组中的元素就是对象的属性
            System.out.println(s[i]);
        }
    }
}
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700471071051-bfd420ca-a64e-4cf8-a4c3-fc296bda844a.png#averageHue=%23f5f4f4&clientId=u4e90e1d7-5d68-4&from=paste&height=616&id=u960ca77d&originHeight=770&originWidth=1987&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=537016&status=done&style=none&taskId=u03376f94-d6fd-4001-8c57-ee15187ab83&title=&width=1589.6)

```java
public class Test01 {
    public static void main(String[] args) {        
        Man[] mans; // 声明
        mans = new Man[10]; // 创建
        Man m1 = new Man(1,11);
        Man m2 = new Man(2,22);
        mans[0] = m1; // 赋值
        mans[1] = m2;
    }
}

class Man{
    private int age;
    private int id;
    public Man(int id,int age){
        super();
        this.age = age;
        this.id = id;
    }
}

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700471664883-f1f062e4-9499-4959-a351-77c01720037e.png#averageHue=%23f4f3f3&clientId=u4e90e1d7-5d68-4&from=paste&height=573&id=ua08acddd&originHeight=716&originWidth=2017&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=514791&status=done&style=none&taskId=uf4facc14-67eb-42ed-a6a0-c6c664d9814&title=&width=1613.6)

<a name="Dfp8R"></a>
### 数组的初始化方式
数组的初始化方式包括：静态初始化、动态初始化、默认初始化。<br />（1）静态初始化<br />除了用new关键字来产生数组外，还可以直接定义数组的同时就为数组元素分配空间并赋值。
```java
int [] a = {1,2,3}; // 静态初始化基本类型数组
Man [] mans = { new Man(1,1), new Man(2,2)}; // 静态初始化引用类型数组
```
（2）动态初始化<br />数组定义与数组元素分配空间并赋值的操作分开进行操作。
```java
int[] s; // 声明数组
s = new int[10]; // 给数组分配空间
for (int i = 0; i < 10; i++){
    s[i] = 2 * i +1; // 给数组元素赋值，数组中的元素就是对象的属性
    System.out.println(s[i]);
}

Man[] mans; // 声明
mans = new Man[10]; // 创建
Man m1 = new Man(1,11);
Man m2 = new Man(2,22);
mans[0] = m1; // 赋值
mans[1] = m2;
```
（3）默认初始化<br />数组是对象，它的元素相当于对象的属性，每个元素也按照属性的方式被默认初始化。
```java
int a2[] = new int[2]; // 默认值：0,0
boolean[] b = new boolean[2]; // 默认值： false,false
String[] s = new String[2]; // 默认值： null,null
```
<a name="MVbFQ"></a>
### 数组的遍历
遍历即通过循环遍历数组所有的元素。元素下标合法区间：[0,length-1]。
```java
int [] arr = new int[10];
for (int i=0; i<arr.length; i++) {
	arr[i] = 100*i
}
```
除此之外，增强for循环for-each是JDK1.5新增的功能，专门用于读取数组或集合中所有元素，即数组进行遍历。
```java
String [] ss = {"aa","bb","ccc","ddd"};
for (String temp:ss){
	System.out.println(temp);
}
```
**注意事项**：

- for-each增强for循环在遍历数组过程中不能修改数组中元素的值。
- for-each仅适用于遍历，不涉及有关索引的操作。
```java
package com.nuobu;

public class Test03 {
    public static void main(String[] args) {
        String[] cities = {"北京","上海","广州","深圳"};
        for(int i=0; i<cities.length;i++){
            String t = cities[i];
            System.out.println(t);
        }
        for(String t:cities){
            System.out.println(t);
        }
    }
}
```
<a name="aNjHH"></a>
### 数组的拷贝
System.arraycopy(object src, int srcpos, object dest, int destpos, int length)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700489114937-55cc226a-779d-4758-b69d-9f664b183057.png#averageHue=%23f6f5e9&clientId=u4e90e1d7-5d68-4&from=paste&height=858&id=u91631bdc&originHeight=1073&originWidth=1874&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1267112&status=done&style=none&taskId=uea493c27-c2e4-46f0-8f33-9479aad2222&title=&width=1499.2)
```java
package com.nuobu;

//测试拷贝
public class Test04 {
    public static void main(String[] args) {
        String [] s = {"阿里","京东","百度","腾讯","字节跳动"};
        String [] sBak = new String[6];
        System.arraycopy(s,0,sBak,0,s.length);
        for (int i = 0; i < sBak.length; i++) {
            System.out.print(sBak[i]+"\t");
        }
    }
}
```
运行结果：<br />阿里	京东	百度	腾讯	字节跳动	null	
<a name="SfwWg"></a>
### 数组操作工具类：Arrays类
```java
package com.nuobu;

import java.util.Arrays;

// 测试Arrays类
public class Test05 {
    public static void main(String[] args) {
        // 输出数组中的元素
        int [] a = {1,2};
        System.out.println(a); // 打印数组引用的值
        System.out.println(Arrays.toString(a)); // 打印数组元素的值
        System.out.println("=================");

        // 对数组元素进行排序
        int [] b = {1,2,323,20,543,12,59};
        System.out.println(Arrays.toString(b));
        Arrays.sort(b);
        System.out.println(Arrays.toString(b));
        System.out.println("=================");

        // 实现二分法查找
        int [] c = {1,2,323,20,543,12,59};
        System.out.println(Arrays.toString(c));
        Arrays.sort(c); // 使用二分法查找，必须先进行排序
        System.out.println(Arrays.toString(c));
        System.out.println("该元素索引：" + Arrays.binarySearch(c,12)); // 返回排序后索引位置，若无则返回负数
        System.out.println("=================");

        // 对数组进行填充
        int [] d = {1,2,323,20,543,12,59};
        System.out.println(Arrays.toString(d));
        Arrays.fill(d,2,4,100); // 将索引[2,4)元素替换为100
        System.out.println(Arrays.toString(d));
    }
}
```
运行结果：<br />[I@723279cf<br />[1, 2]<br />=================<br />[1, 2, 323, 20, 543, 12, 59]<br />[1, 2, 12, 20, 59, 323, 543]<br />=================<br />[1, 2, 323, 20, 543, 12, 59]<br />[1, 2, 12, 20, 59, 323, 543]<br />该元素索引：2<br />=================<br />[1, 2, 323, 20, 543, 12, 59]<br />[1, 2, 100, 100, 543, 12, 59]
<a name="iinJE"></a>
### 多维数组
```java
package com.nuobu;

import java.util.Arrays;

// 多维数组
public class Test06 {
    public static void main(String[] args) {
        int [][] a = new int[3][];
        a[0] = new int[2];
        a[1] = new int[4];
        a[2] = new int[3];

        a[0][0] = 100;

        int [][] b = {
                {1,2,3},
                {3,4},
                {3,5,6,7}
        };

        System.out.println(b[0][2]);
        
        int [][] c = new int [3][];
        c[0] = new int [] {1,2,3};
        c[1] = new int [] {1,3};
        c[2] = new int [] {2,2,5,1,2,3};
        System.out.println(c[2][3]);
        System.out.println(Arrays.toString(c[0]));
    }
}

```
<a name="mOh4B"></a>
### Comparable接口
```java
package com.nuobu;

import java.util.Arrays;

// 测试Comparable接口
public class Test09 {

    public static void main(String[] args) {
        Man2[] msMans = {
                new Man2(3,"a"),
                new Man2(60,"b"),
                new Man2(2,"c"),
        };
        Arrays.sort(msMans);
        System.out.println(Arrays.toString(msMans));
    }
}


class Man2 implements Comparable{
    int age;
    int id;
    String name;

    public Man2(int age,String name){
        super();
        this.age = age;
        this.name = name;
    }

    @Override
    public int compareTo(Object o) {
        Man2 m2 = (Man2) o;
        if(this.age > m2.age)return 1;
        if(this.age < m2.age)return -1;
        return 0;
    }

    @Override
    public String toString() {
        return "Man2{" +
                "name='" + name + '\'' +
                '}';
    }
}
```
<a name="e7YoQ"></a>
### 冒泡排序
两两比较，将较大的交换到后面，直到所有数组元素有序。
```java
package com.nuobu;

import java.util.Arrays;

// 实现冒泡排序
public class TestBubbleSort {
    public static void main(String[] args) {
        int [] values = {3,1,6,8,9,0,7,4,5,2};
        System.out.println("原始顺序：" + Arrays.toString(values));
        bubbleSort(values);
        System.out.println("冒泡后顺序：" + Arrays.toString(values));
    }

    public static void bubbleSort(int[] values) {
        int temp;

        for (int i = 0; i < values.length; i++) {
            boolean flag = false; // 交换标记
            for (int j = 0; j < values.length-1 - i; j++) {
                if (values[j] >= values[j + 1]) {
                    temp = values[j + 1];
                    values[j + 1] = values[j];
                    values[j] = temp;
                    flag = true;
                }
            }
            System.out.println((i+1)+"趟顺序：" + Arrays.toString(values));
            if (!flag) break;
        }
    }
}

```
运行结果：<br />原始顺序：[3, 1, 6, 8, 9, 0, 7, 4, 5, 2]<br />1趟顺序：[1, 3, 6, 8, 0, 7, 4, 5, 2, 9]<br />2趟顺序：[1, 3, 6, 0, 7, 4, 5, 2, 8, 9]<br />3趟顺序：[1, 3, 0, 6, 4, 5, 2, 7, 8, 9]<br />4趟顺序：[1, 0, 3, 4, 5, 2, 6, 7, 8, 9]<br />5趟顺序：[0, 1, 3, 4, 2, 5, 6, 7, 8, 9]<br />6趟顺序：[0, 1, 3, 2, 4, 5, 6, 7, 8, 9]<br />7趟顺序：[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]<br />8趟顺序：[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]<br />冒泡后顺序：[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
<a name="IUjHS"></a>
### 二分查找法
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700557298955-7eb35f49-675f-4620-a978-ec215aa6f386.png#averageHue=%23fdfcfb&clientId=uc13ecd2a-fc5d-4&from=paste&height=298&id=u211962a2&originHeight=790&originWidth=968&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=331553&status=done&style=none&taskId=u6e9ccea5-cd3c-46e8-92c2-4b2ada94ef2&title=&width=365.4000244140625)<br />二分查找对有序序列进行查找。找到返回索引下表，否则返回-1。
```java
package com.nuobu;

import java.util.Arrays;

public class TestBinarySearch {
    public static void main(String[] args) {
        int [] arr = {30,20,50,10,80,9,7,15,12,100,14,40,8,4};
//        4, 7, 8, 9, 10, 12, 14, 15, 20, 30, 40, 50, 80, 100
        int searchWord = 100; // 要查找的数
        Arrays.sort(arr);

        System.out.println(Arrays.toString(arr));
        System.out.println(searchWord+"元素的索引：" + binarySearch(arr,searchWord));
    }

    public static int binarySearch(int arr[], int value){
        int low = 0;
        int high = arr.length - 1;
        int mid;
        while(high >= low){
            mid = (low+high)/2;
            if (arr[mid] == value) return mid;
            if (arr[mid] < value) low = mid + 1;
            if (arr[mid] > value) high = mid - 1;
        }
        return -1;
    }

}

```

