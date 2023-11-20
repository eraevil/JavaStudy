<a name="gfeMi"></a>
## 抽象类和接口
<a name="CqiQ0"></a>
### 抽象方法和抽象类 abstract
（1）抽象方法使用abstract修饰，没有方法体，只有声明。定义的是一种规范，告诉子类必须要给抽象方法提供具体的实现。<br />（2）包含抽象方法的类就是抽象类。通过抽象类，做到严格限制子类的设计，使子类之间更加通用。
```java
package com.nuobu.abstractClass;

public abstract class Animal {
    int age;
    public abstract void rest();
    public abstract void run();
    public void shout(){
        System.out.println("Animal.shout");
    }
}

class Dog extends Animal{
    @Override
    public void rest() {
        System.out.println("Dog.rest");
    }

    @Override
    public void run() {
        System.out.println("Dog.run");
    }
}


class Cat extends Animal{
    @Override
    public void rest() {
        System.out.println("Cat.rest");
    }

    @Override
    public void run() {
        System.out.println("Cat.run");
    }
}
```
（3）使用要点

- 有抽象方法的类只能定义为抽象类。
- 抽象类不能实例化，即不能使用new来实例化抽象类。
- 抽象类可以包含属性、方法、构造方法。但是构造方法不能用来new实例，只能用来被子类调用。
- 抽象类只能用来被继承。
- 抽象方法必须被子类实现。
<a name="QvPiU"></a>
### 接口 interface
<a name="ag6mU"></a>
#### 基本概念
接口就是一组规范，所有实现类都要遵守。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700444190732-7534312e-45f3-481c-a84e-816209629e9c.png#averageHue=%23eeedec&clientId=ua141d37f-12a4-4&from=paste&height=757&id=uf9d108c6&originHeight=946&originWidth=2035&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=1541013&status=done&style=none&taskId=u67633867-9bec-46ad-ac68-ca5c440f1fb&title=&width=1628)
```java
public interface Runnable {
    // 常量定义 public static final
    // 方法定义 public abstract
    // 接口可继承其他接口。
}
```
使用要点：

- 子类通过implements来实现接口中的规范。
- 接口不能创建实例，但是可以用于声明引用变量的类型。
- 一个类实现了接口，必须实现接口中所有的方法，且都是public方法。
```java
// ======================接口====================
package com.nuobu.testInterface;

// 飞行接口
public interface Volant {
    int Fly_HIGHT = 100; // public static final
    void fly(); // public abstract
}

// 善良接口
interface Honest{
    void helpOhter();
}

// 好人类
class GoodMan implements Honest{
    @Override
    public void helpOhter() {
        System.out.println("扶老奶奶过马路");
    }
}

// 鸟人
class BirdMan implements Volant{
    @Override
    public void fly() {
        System.out.println("BirdMan.fly");
    }
}

// 天使类
class Angel implements Volant,Honest{
    @Override
    public void fly() {
        System.out.println("Angel.fly");
    }

    @Override
    public void helpOhter() {
        System.out.println("Angel.helpOhter");
    }
}


// 飞机类
class Plane implements Volant{
    @Override
    public void fly() {
        System.out.println("Plane.fly");
    }
}

// ===================测试接口===================
package com.nuobu.testInterface;

public class Test {
    public static void main(String[] args) {
        Angel a = new Angel();
        a.fly();
        a.helpOhter();
        System.out.println(a.Fly_HIGHT);

        Volant a2 = new Angel();
        a2.fly();
        // a2.helpOhter(); // 需要转型

    }
}

```
<a name="FNefD"></a>
#### 接口的默认方法和静态方法
JDK8之前，接口里的方法全是抽象方法，从JDK8开始，允许在接口里定义默认方法和静态方法。默认方法，即允许给接口添加一个非抽象的方法实现，只需要使用**default**关键字即可，也称为扩展方法（在标准下的默认实现）。**抽象方法必须被实现，默认方法不是，作为替代方式，接口实现类都可以得到默认方法。**
```java
package com.nuobu.testInterface;

// 测试接口中的新特性（默认方法、静态方法）
public interface TestDefault {
    void printInfo();
    // 默认方法
    default void moren(){
        System.out.println("TestDefault.moren");
        System.out.println("测试默认方法！");
    }

    // 接口的静态方法
    public static void testStatic01(){
        System.out.println("TestDefault.testStatic01");
    }
}

class TestDefaultImpl01 implements TestDefault{
    @Override
    public void printInfo() {
        System.out.println("TestDefaultImpl01.printInfo");
    }

    // 实现类的静态方法，与接口的完全不同
    public static void testStatic01(){
        System.out.println("TestDefaultImpl01.testStatic01");
    }
}


// ============测试================
System.out.println("==========测试默认方法==========");
TestDefault td = new TestDefaultImpl01();
td.printInfo();
td.moren();
// ================================
```
运行结果：<br />==========测试默认方法==========<br />TestDefaultImpl01.printInfo<br />TestDefault.moren<br />测试默认方法！

接口中如果定义了静态方法，这个方法属于接口，可以通过接口名直接调用。如果实现类中定义了相同名字的静态方法，那就是完全不同的方法，是直接从属于子类的方法，通过子类名进行调用。（**不是重写！！！**）<br />**默认方法中可以调用静态方法，静态方法中不能调用默认方法。**
```java
System.out.println("==========测试静态方法==========");
TestDefault.testStatic01();
TestDefaultImpl01.testStatic01();
```
运行结果：<br />==========测试静态方法==========<br />TestDefault.testStatic01<br />TestDefaultImpl01.testStatic01
<a name="GkJXC"></a>
#### 接口的多继承
接口支持多继承。和类的继承类似，子接口extends父接口，会获得父接口的一切。下图中销售经理就是多继承。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700447398512-bea0b146-5a96-4b34-abab-c481c163e801.png#averageHue=%23f8f8f8&clientId=u73742ebf-564a-4&from=paste&height=527&id=u5b57e496&originHeight=659&originWidth=1138&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=253940&status=done&style=none&taskId=u2400ca66-7fbf-4262-b4f5-374d58dd58f&title=&width=910.4)

```java
package com.nuobu.testInterface;

// 测试接口多继承
public class TestMultipleInheritance {
    public static void main(String[] args) {
        C c = new CImpl01();
        c.testA();
        c.testB();
        c.testC();
    }
}


interface A{
    void testA();
}

interface B{
    void testB();
}

interface C extends A,B {
    void testC();
}

class CImpl01 implements C {
    @Override
    public void testA() {    }
    @Override
    public void testB() {    }
    @Override
    public void testC() {    }
}
```


<a name="E6rcg"></a>
## 字符串String类
<a name="nZswu"></a>
### String类的本质
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700449772511-66477d7a-d2d6-4118-8444-f6680ddc414d.png#averageHue=%23f1f1f0&clientId=u16fdd49d-c65b-4&from=paste&height=454&id=u9b37fc61&originHeight=568&originWidth=1924&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=799129&status=done&style=none&taskId=u228053f3-0b1a-4ad1-b2fb-48f0c3b3126&title=&width=1539.2)<br />本质是一个不可变的数组。
```java
private final byte[] value;
```
<a name="F8Pu4"></a>
### String类和常量池
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700450537130-87576d17-12be-4a9b-b794-d88baaa0968d.png#averageHue=%23f0efee&clientId=u16fdd49d-c65b-4&from=paste&height=228&id=u0605290a&originHeight=285&originWidth=1948&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=426792&status=done&style=none&taskId=u498bd22b-2159-4f26-921c-c21742bd262&title=&width=1558.4)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700450693052-f638dbc0-1b60-4c73-9071-8d8954f09a84.png#averageHue=%23d0f7a4&clientId=u16fdd49d-c65b-4&from=paste&height=796&id=uba0e359b&originHeight=995&originWidth=1686&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=712486&status=done&style=none&taskId=u88be48d5-ce99-4910-b28a-aa73bc712ae&title=&width=1348.8)<br />常见的String类方法：
```java
String s1 = "core Java";
String s2 = "Core Java";
System.out.println(s1.charAt(3)); // 返回下标为3的字符
System.out.println(s2.length());// 字符串长度
System.out.println(s1.equals(s2));// 比较两个字符串
System.out.println(s1.equalsIgnoreCase(s2)); // 比较两个字符串，忽略大小写
System.out.println(s1.indexOf("Java")); // s1中是否包含Java,返回索引位置
System.out.println(s1.indexOf("APPLE"));//s1中是否包含APPLE,返回-1
String s = s1.replace(' ','&');//将空格替换为&
System.out.println(s);

s = "";
s1 = "How are you?";
System.out.println(s1.startsWith("How")); // 是否以How开头
System.out.println(s1.endsWith("you")); // 是否以you结尾
s = s1.substring(4); // 提取字符串：从下标4开始到字符串结尾
System.out.println(s);
s = s1.substring(4,7); // 提取字符串：从下标4开始到7,不包括7:[4,7)
System.out.println(s);
s = s1.toLowerCase(); // 转小写
System.out.println(s);
s = s1.toUpperCase(); // 转大写
System.out.println(s);
s2 = "  How old are you!!  ";
s = s2.trim(); // 去除首尾空格，保留字符串中间空格
System.out.println(s);
System.out.println(s2); // 未改变s2自身

String s3 = "I Love java. java is best language!";
System.out.println(s3.indexOf("java"));  // 7
System.out.println(s3.lastIndexOf("java")); // 13
```
<a name="EhkTS"></a>
## 内部类
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700463595368-6aaac8ef-c93d-49b9-9a39-6ee1779f3888.png#averageHue=%23f4edd6&clientId=u16fdd49d-c65b-4&from=paste&height=444&id=u53511b83&originHeight=555&originWidth=1454&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=373352&status=done&style=none&taskId=uceb6efb5-0370-4c8b-b4d0-96e3ac87819&title=&width=1163.2)<br />内部类提供了更好的封装。只能让外部类直接访问，不允许同一个包中的其他类直接访问。内部类可以直接访问外部类的私有属性，内部类被当成其外部类的成员。但外部类不能访问内部类的内部属性。<br />内部类是一个编译时概念，一旦编译成功，就会成为两个完全不同的类。一个名为Outer的外部类和其内部定义的内部类Inner，编译完成后会产生Outer.class和Outer$Inner.class两个类的字节码。所以内部类是相对独立的一种存在，其成员变量/方法名可以和外部类相同。
```java
package com.nuobu.InnerClass;

public class Outer {
    private int age = 10;
    public static void main(String[] args) {}
    public void show(){
        System.out.println("Outer.show");
        System.out.println(age);
    }
    
    public class Inner{
        int age = 20;
        public void show(){
            System.out.println(age);
        }
    }
}

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1700465303586-414194e1-7c86-4962-8bf2-f470096471a3.png#averageHue=%23fcfcfb&clientId=u16fdd49d-c65b-4&from=paste&height=111&id=ua8e9f4b7&originHeight=139&originWidth=1042&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=12492&status=done&style=none&taskId=u3bc310a2-a9f1-405f-985e-aa4abd855ad&title=&width=833.6)
<a name="iey6E"></a>
### 非静态内部类
（1）非静态内部类对象必须寄存在一个外部类对象里。因此，如果有一个非静态内部类对象那么一定存在对应的外部类对象。非静态内部类对象单独属于外部类的某个对象。<br />（2）非静态内部类可以直接访问外部类的成员，但是内部类不能直接访问非静态内部类成员。<br />（3）非静态内部类不能有静态方法、静态属性和静态初始化块。<br />（4）成员访问要点：

- 内部类属性：this.变量名。
- 外部类属性：外部类名.this.变量名。
```java
package com.nuobu.InnerClass;

public class Outer {
    private int age = 10;
    public static void main(String[] args) {}
    public void show(){
        System.out.println("Outer.show");
        System.out.println(age);
    }

    public class Inner{
        int age = 20;
        public void show(){
            System.out.println(age);
            System.out.println(Outer.this.age);
            Outer.this.show();
        }
    }
}
```
（5）内部类的访问：

- 外部类中定义内部类： new Inner()
- 外部类以外的地方使用非静态内部类： Outer.Inner varname = new Outer().new Inner()
```java
package com.nuobu.InnerClass;

public class Outer {
    private int age = 10;
    public static void main(String[] args) {
        Inner i = new Outer().new Inner(); // 静态方法和外部类以外的地方使用非静态内部类
        i.show();
    }
    public void show(){
        System.out.println("Outer.show");
        System.out.println(age);
        Inner i1 = new Inner(); // 外部类中定义内部类
    }

    public class Inner{
        int age = 20;
        public void show(){
            System.out.println(age);
            System.out.println(Outer.this.age);
            Outer.this.show();
        }
    }
}
```
运行结果：<br />20<br />10<br />Outer.show<br />10
<a name="am2t7"></a>
### 静态内部类
静态内部类可以访问外部类的静态成员，不能访问外部类的普通成员。<br />静态内部类看作外部类的一个静态成员。
```java
package com.nuobu.InnerClass;

class Outer2{
    private int a = 10;
    private static int b = 20;
    // 相当于外部类的一个静态成员
    static class Inner2{
        public void test(){
            // System.out.println(a); // 静态内部类不能访问外部类的普通属性
            System.out.println(b); // 静态内部类可以访问外部类的静态属性
        }
    }
}

public class TestStaticInnerClass {
    public static void main(String[] args) {
        // 通过new 外部类.内部类名（） 来创建内部类对象
        Outer2.Inner2 inner = new Outer2.Inner2();
        inner.test();
    }
}
```
<a name="ZJ4Bq"></a>
### 匿名内部类
适合只需要使用一次的类。比如：键盘监听操作等。在安卓开发、awt、swing开发中常见。
```java
package com.nuobu.InnerClass;

public class TestAnonymousInnerClass {
    public void test1(A a){
        a.run();
    }

    public static void main(String[] args) {
        TestAnonymousInnerClass t = new TestAnonymousInnerClass();
        // t.test1(new AImpl()); // 使用匿名内部类就不需要如此调用
        t.test1(new A(){  // 创建一个没有名字的A的实现类
            @Override
            public void run() {
                System.out.println("第一个匿名内部类");
            }
        });
        t.test1(new A(){  // 创建一个没有名字的A的实现类
            @Override
            public void run() {
                System.out.println("第二个匿名内部类");
            }
        });

    }
}

interface A{
    void run();
}

// 使用匿名内部类就不需要如此定义
//class AImpl implements A{
//    @Override
//    public void run() {
//        System.out.println("AImpl.run");
//    }
//}

```
