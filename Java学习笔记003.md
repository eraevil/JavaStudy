<a name="gfeMi"></a>
## 包机制（package、import)
包相当于文件夹对于文件的作用。用于管理类、解决类的重名的问题。<br />package的使用有两个要点：<br />（1） 通常是类的第一句非注释性语句。<br />（2） 包名：域名倒着写即可，再加上模块名，便于内部管理类。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699447882395-4bf71ffe-7f29-4522-a3a0-5eb4faf5eb41.png#averageHue=%23e4e4e3&clientId=ub2a64108-6be3-4&from=paste&height=140&id=u93ddd420&originHeight=262&originWidth=1559&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=241527&status=done&style=none&taskId=u5f715e07-c5f2-4793-b698-27bca0f737f&title=&width=831.4666666666667)
<a name="CqiQ0"></a>
### JDK中主要的包
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699448130440-f8d4e705-3f24-4181-8b2a-b48df4d0f3ee.png#averageHue=%23d1ddb7&clientId=ub2a64108-6be3-4&from=paste&height=225&id=u1335e90a&originHeight=422&originWidth=1558&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=520531&status=done&style=none&taskId=u7df4e780-b4a1-439a-aed9-bae3dc7c64f&title=&width=830.9333333333333)
<a name="h0lZs"></a>
### 导入包
如果需要使用其他包的类，需使用import，从而在本类中直接通过类名来调用，否则就需要书写类的完整包名和类名。
```java
// ======================com.nuobu.oop.Car=======================
package com.nuobu.oop;

public class Car {
    public static void main(String[] args) {
    }
}

// =====================com.nuobu.test.TestImport=================
package com.nuobu.test;
import com.nuobu.oop.Car;

public class TestImport {
    public static void main(String[] args) {
        com.nuobu.oop.Car car = new com.nuobu.oop.Car(); // 如果不import，需要这样调用
        Car car1 = new Car();
    }
}

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699448873926-9696032c-7304-4c24-ba34-dfd5306233a3.png#averageHue=%23e2e1e1&clientId=u39d827d9-65fd-4&from=paste&height=132&id=u2bba7100&originHeight=248&originWidth=1490&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=282795&status=done&style=none&taskId=ud4cd193d-0cc2-422d-a1ff-b19920acd7b&title=&width=794.6666666666666)
```java
import java.util.*; // 导入该包下所有的类。会降低编译速度，但不会降低运行速度。
```
**静态导入**<br />static import ，其作用是用于导入指定类的静态属性和静态方法，这样我们能直接使用静态属性和静态方法。
```java
package com.nuobu.test;
import static java.lang.Math.*; // 导入Math类的所有静态属性
import static java.lang.Math.PI; // 导入Math类的PI属性

public class TestStaictImport {
    public static void main(String[] args) {
        System.out.println(PI);
        System.out.println(random());
    }
}
```
执行结果：
:::info
3.141592653589793<br />0.8317435314403968
:::
<a name="qFvbj"></a>
## 面向对象三大特征：继承、封装、多态
<a name="MSeui"></a>
### 继承 extends
<a name="XjQAs"></a>
#### 基本概念

- 继承的主要作用是：（1）代码复用，更加容易实现类的扩展。（2）方便建模。
```java
class Person {
    String name;
    double height;
    public void rest(){
        System.out.println("休息！");
    }
}

class Student extends Person{
    String major;

    public void study(){
        System.out.println("学习！");
        rest();
        System.out.println(this.name);
    }

    public Student(String name,double height,String major){
        this.name = name;
        this.height = height;
        this.major = major;
    }
}
```

- 父类也称作超类、基类。子类称为派生类。
- Java中只有单继承，没有像C++那样的多继承。多继承会引发混乱，使得继承链过于复杂，系统难以维护。
- Java中类没有多继承，接口有多继承。
- **子类继承父类，可以得到父类的全部属性和方法（除了父类的构造方法），但不见得可以直接访问（比如，父类私有的属性和方法）。**
- 如果定义一个类时，没有调用extends，则它的父类是java.lang.Object。
<a name="iAHQd"></a>
#### 方法重写override
子类可以重写父类的方法，可以用自身行为替换父类行为。**重写是实现多态的必要条件。**方法重写需要符合下面三个要点：<br />(1) "=="：方法名，形参列表相同。<br />(2) "≤"：返回值类型和声明异常类型，子类小于等于父类。<br />(3) "≥"：访问权限，子类大于等于父类。
```java
package com.nuobu.oop;

public class TestOverride {
    public static void main(String[] args) {
        Horse h = new Horse();
        h.run();
        h.getVehicle();
    }
}

class Vehicle{ // 交通工具类
    public void run(){
        System.out.println("跑！！！！！！");
    }

    public Vehicle getVehicle(){
        System.out.println("给你一个交通工具！");
        return null;
    }
}

class Horse extends  Vehicle{ // 马继承交通工具类
    @Override
    public void run(){ // 重写，方法名，形参列表相同。
        System.out.println("滴滴答答地跑！");
    }

    public Vehicle getVehicle(){
        System.out.println("给一匹马。。");
        return new Horse(); // 返回值类型，子类小于等于父类。
    }
}

class Plane extends Vehicle { // 飞机继承交通锅具类
    @Override
    public void run(){
        System.out.println("天上飞。");
    }
}

```
<a name="wz2bJ"></a>
#### final关键字
final关键字的作用

- **修饰变量**：该变量不可改变。一旦赋了初值，就不能重新赋值。
```java
final int MAX_SPEED = 120;
```

- **修饰方法**：该方法不可被重写。但可以被重载。
```java
final void study(){
    System.out.println("1111");
};
final void study(int a){
    System.out.println("222");
};
```

- **修饰类**：修饰的类不能被继承。比如Math、String等。
```java
final class A {}
```
<a name="feHDX"></a>
#### 继承和组合
除了继承，组合也能实现代码的复用，核心是“将父类对象作为子类的属性”。
```java
class Person2 {
    String name;
    double height;
    public void rest(){
        System.out.println("休息！");
    }
}

class Student2 {
    String major;
    
    // 利用组合的方式，将Person类对象作为Student的属性。
    Person2 person2 = new Person2(); 
	
    
    public void study(){
        System.out.println("学习！");
        person2.rest();
        System.out.println(this.person2.name);
    }

    public Student2(String name,double height,String major){
        this.person2.name = name;
        this.person2.height = height;
        this.major = major;
    }
}
```
组合比较灵活。继承只能有一个父类，但是组合可以有多个属性。<br />但是，不能因为组合而完全舍弃继承。**对于“is-a”关系用继承，“has-a”关系用组合。**<br />对于上述例子，Student is a Person，应该用继承，而不是Student has a Person，组合是不合适的。而“笔记本”和“芯片”的关系显然是“has-a”，使用组合更好。
<a name="aa810"></a>
#### Object类
Object是所有类的父类，所有Java对象都拥有Object类的属性和方法。<br />在类的声明中未继承别的类，则默认继承Object类。<br />**（1）toString方法的重写**
```java
package com.nuobu.oop;

public class TestObject extends Object{
    String name;
    String pwd;

    public static void main(String[] args) {
        TestObject t = new TestObject();
        System.out.println(t.toString());
    }

    @Override
    public String toString() {
        return "账户名："+name+" 密码："+pwd;
    }
}
```
**（2）equals方法的重写**

- "=="比较双方是否相同。在基本类型中表示值相等，引用类型表示同一个地址，即指向同一个对象。
- equals()提供“对象内容相等”的逻辑。默认的equals()比较两个对象的hashcode，可以根据需求重写equals。
```java
public class TestObject extends Object{
    int id;
    String name;
    String pwd;
    
    public static void main(String[] args) {
        TestObject t1 = new TestObject(1001,"zhangsan","123456");
        TestObject t2 = new TestObject(1001,"lisi","123456");
        TestObject t3 = new TestObject(1002,"zhangsan","123456");
        System.out.println("t1 equals t2 ? " + t1.equals(t2));
        System.out.println("t2 equals t3 ? " + t2.equals(t3));
    }
    
    @Override
    public boolean equals(Object o) {
        if(this == o) return true;
        if(o==null || getClass() != o.getClass()) return false;
        TestObject that = (TestObject) o;
        return (this.id == that.id);
    }

    ......
}
```
运行结果：<br />t1 equals t2 ? true<br />t2 equals t3 ? false

**（3）super关键字**

- super可以看作是直接父类对象的引用。可以通过super来访问父类中被子类覆盖的方法或属性。
- 使用super调用普通方法，语句没有位置限制，可以在子类中随便调用。
```java
package com.nuobu.oop;

public class TestSuper01 {
    public static void main(String[] args) {
        new ChildClass().f();
    }
}


class FatherClass{
    public int value;
    public void f(){
        value = 100;
        System.out.println("FatherClass.value="+value);
    }
}

class ChildClass extends FatherClass{
    public int value;
    public int age;
    public void f(){
        super.f(); // 调用父类的普通方法
        value = 200;
        System.out.println("ChildClass.value="+value);
        System.out.println(value);
        System.out.println(super.value);
    }
    public void f2(){
        System.out.println(age);
    }
}
```
运行结果：<br />FatherClass.value=100<br />ChildClass.value=200<br />200<br />100

- **在一个类中，若是构造方法的第一行没有调用super(...)或者this(...)；那么Java默认都会调用super()，含义是调用父类的无参构造方法。所以继承关系中，子类对象的创建首先会向上追溯，直到利用Object的无参构造方法，然后依次向下执行类的初始化块和构造方法，直到当前子类为止。**
- 静态初始块的调用顺序与构造方法调用顺序一样。
```java
package com.nuobu.oop;

public class TestSuper02 {
    public static void main(String[] args) {
        new ChildClass2();
    }
}

class FatherClass2{
    static {
        System.out.println("静态初始化：FatherClass2");
    }
    public FatherClass2(){
        System.out.println("创建对象：FatherClass2");
    }
}

class ChildClass2 extends FatherClass2{
    static {
        System.out.println("静态初始化：ChildClass2");
    }
    public ChildClass2(){
        System.out.println("创建对象：ChildClass2");
    }
}
```
运行结果：<br />静态初始化：FatherClass2<br />静态初始化：ChildClass2<br />创建对象：FatherClass2<br />创建对象：ChildClass2

<a name="EQmJX"></a>
### 封装 encapsulation
<a name="wfbGr"></a>
#### 基本概念
封装的理念：高内聚、低耦合。高内聚指类的内部数据操作细节自己完成，不允许外部干涉。低耦合是仅暴露少量的方法给外部使用，尽量方便外部调用。具有以下优点：<br />（1）提高代码安全性。<br />（2）提高代码复用性。<br />（3）“高内聚”：封装细节，便于修改内部代码，提高可维护性。<br />（4）“低耦合”：简化外部调用，便于调用者使用，便于扩展和协作。<br />Java通过使用访问控制符来控制实现细节的封装。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699513020467-c8cf5c18-3835-4a62-9dfd-137a09783829.png#averageHue=%23c7d7a3&clientId=ubd00da3d-eced-4&from=paste&height=202&id=u12ca38ab&originHeight=379&originWidth=1096&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=187138&status=done&style=none&taskId=ud4f38c1b-61f0-455f-ba4c-f3e248877d6&title=&width=584.5333333333333)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699513118067-b35c94e0-6d9c-41a8-a6e9-b5f7e2c25f4d.png#averageHue=%23f7f4df&clientId=ubd00da3d-eced-4&from=paste&height=345&id=u9c5bd2f9&originHeight=646&originWidth=797&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=437661&status=done&style=none&taskId=u6ef0bfe2-8b00-4887-ac0a-4bc85a8c40e&title=&width=425.06666666666666)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699514073922-663f995c-0c0d-41b9-924e-e8fc8f6c8678.png#averageHue=%23eeeeee&clientId=ubd00da3d-eced-4&from=paste&height=181&id=uc254dcbd&originHeight=339&originWidth=1557&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=286611&status=done&style=none&taskId=u3c92c1a8-dfcd-44bd-8ad5-5161e022dcf&title=&width=830.4)
<a name="sipsa"></a>
#### 开发中封装的简单规则
（1）属性一般使用private访问权限。<br />属性私有后，提供相应的get/set方法来访问相关属性，这些方法通常是public修饰的，以提供对属性的赋值和读取操作（注意：boolean）<br />（2）方法：一些只用于本类的辅助性方法可以用private修饰，希望其他类调用的方法用public修饰。
```java
package com.nuobu.encapsulation.b;
// Javabean
public class User {
    private int id;
    private String name;
    private boolean man;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public boolean isMan() {
        return man;
    }

    public void setMan(boolean man) {
        this.man = man;
    }
}

package com.nuobu.encapsulation.b;
public class Test {
    public static void main(String[] args) {
        User u = new User();
        u.setId(1001);
        u.setName("nuobu");
        u.setMan(true);

        System.out.println(u.getId());
        System.out.println(u.getName());
        System.out.println(u.isMan());
    }
}

```
<a name="fI8Kn"></a>
### 多态 polymorphism

