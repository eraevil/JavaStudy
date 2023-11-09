## 面向对象OOP
面向对象是“设计者思维”，需求中，名词往往抽象为类，再挖掘属性和对应的行为。面向过程是“执行者思维”，关注实现的步骤。
### 类和对象（类相当于图纸，对象是实例）

- 一个Java文件可以定义多个类。
- 类有三个成员：属性，方法，构造器。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699276165771-85988e00-efcb-4a68-86f5-47caf08004c5.png#averageHue=%23f1f1ef&clientId=uaa52b90f-b39b-4&from=paste&height=365&id=u1312d354&originHeight=828&originWidth=1571&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=494994&status=done&style=none&taskId=u28fad7ee-68f5-4688-89ca-31737b03d01&title=&width=692.2650756835938)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699276238845-39af35fd-0be1-4420-ac49-e1987edb6179.png#averageHue=%23f2f2f2&clientId=uaa52b90f-b39b-4&from=paste&height=355&id=u74c22262&originHeight=585&originWidth=1534&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=332802&status=done&style=none&taskId=u9de611e8-0085-460a-949d-8979edd4bf5&title=&width=929.6969159619351)

- **构造器用于对象的初始化，而不是创建对象。**

![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699277329512-eab8522f-cece-4f94-9c20-0a51ca563a14.png#averageHue=%23f2eaea&clientId=uaa52b90f-b39b-4&from=paste&height=341&id=u751ac380&originHeight=563&originWidth=971&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=175599&status=done&style=none&taskId=u180c8fa8-d8ab-42ba-935c-bc8142d9de7&title=&width=588.4848144713422)
```java
修饰符 类名(形参列表){
    // 语句
}
```
**构造器通过new关键字调用**。<br />构造器虽然有返回值，但是不能定义返回值类型（**因为返回值必定是本类**），不能再构造器里使用return返回某个值。<br />**如果不定义构造器，不是没有，而是系统编译器自动定义了一个无参的构造方法**，你这懒狗。如果已经定义，则不再自动添加。<br />**构造器的方法名必须与类名一致**！
## JAVA虚拟机内存模型
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699364095358-c75c7493-d02b-4523-a443-d38813f93820.png#averageHue=%23e1ebda&clientId=u1338372b-05b7-4&from=paste&height=485&id=ue7b69d11&originHeight=801&originWidth=1140&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=499460&status=done&style=none&taskId=u4415cb41-4cec-4146-9b7b-c5909076eab&title=&width=690.9090509756232)
### 虚拟机栈

- 栈描述的是方法执行的内存模型。每个方法被调用都会创建一个栈帧（存储局部变量、操作数、方法出口等）
- **JVM为每个线程创建一个栈**，用于存放该线程执行方法的信息（实际参数、局部变量等）
- **栈属于线程私有**，不能实现线程间的共享。
- 栈的存储特性是“先进后出，后进先出”。
- 栈是由系统自动分配，速度块。栈是一个连续的内存空间。
### 堆

- 堆用于存储创建好的对象和数组（数组也是对象）。
- **JVM只有一个堆，被所有线程共享。**
- 堆不是一个连续的内存空间，分配灵活，速度慢。
- 堆被所有线程所共享，在堆上的区域，会被垃圾回收器做进一步的划分，例如新生代、老年代的划分。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699409798710-d37e4816-43d5-4249-b762-3911b19063b3.png#averageHue=%23d8d6d3&clientId=u1338372b-05b7-4&from=paste&height=89&id=ubd227387&originHeight=200&originWidth=625&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=41134&status=done&style=none&taskId=u090e7bc2-705c-4ea8-852e-c9d8a599e85&title=&width=277.77777777777777)
### 方法区（本质也是堆）

- 方法区是JAVA虚拟机规范，可以有不同的实现。
   - JDK7以前是“永久代”。
   - JDK7部分去除“永久代”，静态变量、字符串常量池都挪到了堆内存中。
   - JDK8是“元数据空间”和堆结合起来。
- **JVM只有一个方法区，被所有线程共享。**
- 方法区实际也是堆，只是用于存储类、常量相关的信息。
- 用来存放程序中永远不变或者唯一的内容。（**类信息、静态变量、字符串常量等**）。
- 常量池主要存放常量：如文本字符串、final常量值。
### 参数传值、赋值机制

- Java中，**方法中所有参数都是“值传递”**，也就是“传递的是值的副本”。副本的改变不会影响原值。
- 基本类型参数的传值，**传递值的副本**，改变不影响原值。
- 引用类型参数的传值，**传递值的副本**，但引用类型的值是“对象的地址”，因此正本和副本都指向同一个对象的地址，改变会改变原值。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699411821602-39df445d-4105-40de-8c52-03007c19e234.png#averageHue=%239af898&clientId=u1338372b-05b7-4&from=paste&height=268&id=ufac62874&originHeight=603&originWidth=1605&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=524024&status=done&style=none&taskId=u728ec733-ab60-45f7-9da1-6d3fd468e93&title=&width=713.3333333333334)
## JAVA垃圾回收机制
### 内存管理

- **Java的内存管理**：主要是**堆中对象的管理**。其中包括对象空间的分配和释放。
- **对象空间的分配**：使用new关键字创建对象即可。
- **对象空间的释放**：将对象赋值null即可。
### 垃圾回收过程
任何一种垃圾回收算法一般要做两件基本的事情：

- **发现无用的对象。**
- **回收无用对象所占用的内存空间。**

垃圾回收机制保证可以将“无用的对象”进行回收。<br />无用的对象指，没有任何变量引用该对象。Java的垃圾回收器通过相关算法发现无用对象，并进行清除和整理。
### 垃圾回收算法
#### 引用计数法
堆中每一个对象都对应一个引用计算器，当有引用指向这个对象时，引用计数器+1。而当指向该对象的引用失效时（引用变为null），引用计数器-1。当引用计数器为0时，Java回收器判定其为无用的对象，回收并释放空间。算法简单，**缺点是循环引用的无用对象无法识别**。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699427064529-bb56004d-35de-4223-81d4-e3152fa8de5f.png#averageHue=%23d3dbee&clientId=uceabd04f-515f-4&from=paste&height=216&id=u789ab95b&originHeight=485&originWidth=671&originalType=binary&ratio=2.25&rotation=0&showTitle=false&size=320073&status=done&style=none&taskId=uf84e1cb3-7ea0-4df5-a3c9-e47feab8879&title=&width=298.22222222222223)
```java
/**
 * 循环引用示例
 * */
public class Student {
    String name;
    Student friend;

    public static void main(String[] args) {
        Student s1 = new Student();
        Student s2 = new Student();

        s1.friend = s2;
        s2.friend = s1;

        s1 = null;
        s2 = null;
    }
}
```
#### 引用可达法
程序把所有引用关系看作一张图，从一个节点GC ROOT开始，寻找对应的引用节点，找到这个节点后，继续寻找这个节点的引用节点，当所有的引用节点寻找完毕后，剩余的节点则被认为是没有被引用的节点，即无用的节点。（未解）
### 通用的分代垃圾回收机制
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699427853222-9f7f83a1-cde4-46d9-80cd-333bb53d69ce.png#averageHue=%23c3f399&clientId=uceabd04f-515f-4&from=paste&height=287&id=u7f2ac415&originHeight=605&originWidth=1112&originalType=binary&ratio=2.25&rotation=0&showTitle=false&size=322905&status=done&style=none&taskId=u3e2a57c1-bfe2-4e07-8060-dacf0c302a5&title=&width=528.1111145019531)
#### 一个对象的在垃圾回收过程中的一生
被创建出来的对象会放入堆中的年轻代的Eden区，Eden区大于装满了（如100个对象），会触发一次Minor GC，这个工作做的是，将年轻代中Eden区和Survivor区的无用对象清除，并将剩余的Eden区中的对象复制到survivor1区，survivor1区中的剩余对象复制到2区，2区中对象复制到1区。将活过15次的对象扔到老年代Tenured区里去。在年老代中等着被Major GC或Full GC干掉。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699429424621-87a9da8f-5371-4fc2-86a8-bed23ba671ef.png#averageHue=%23e7e6e3&clientId=uceabd04f-515f-4&from=paste&height=272&id=u741efddf&originHeight=510&originWidth=880&originalType=binary&ratio=2.25&rotation=0&showTitle=false&size=252196&status=done&style=none&taskId=u488ff8d8-6d1e-4df8-8c24-03876d4468f&title=&width=469.3333333333333)<br />Minor GC：迅速收割生命周期短的无用对象。采用频繁操作的复制算法，效率较高，但是会耗费内存空间。<br />Major GC：会对老年代中的对象进行清除，去除掉无用的对象。<br />Full GC：会对年轻代、老年代、永久代Perm区域进行清除，会对系统性能造成影响。
#### JVM调优和Full GC
在JVM调优过程中，很大一部分工作就是对Full GC的调节。有以下原因**可能**导致Full GC:

- 年老代被写满。
- 永久代被写满。
- System.gc()被显示调用。（可能会触发，程序员儿只有建议权，没有决定权）
- 上一次GC之后Heap的各区域分配策略动态变化。
#### 开发中常见的内存泄漏操作
内存泄漏：指堆内存中由于某种原因程序未释放，造成内存浪费，导致运行速度减慢甚至系统崩溃。<br />**(1) 创建大量无用对象。**
```java
// 大量拼接字符串，使用了String而不是StringBuilder
String str = "";
for(int i = 0; i < 100000; i++) {
    str += i;  // 相当于产生了100000个Srting对象
}
```
**(2) 静态类合计的使用。**<br />像HashMap、Verctor、List等的使用也容易出现内存泄漏，这些静态变量的生命周期和应用程序一致，所有的对象也不能被释放。<br />**(3) 各种连接对象（IO流对象、数据库连接对象、网络连接对象）未关闭。**<br />这些对象属于物理连接，和硬盘或者网络硬件资源关联，不使用时一定要关闭。<br />**(4) 监听器的使用不当。**释放对象时，没有删除相应的监听器。
#### 其他要点
(1) 程序员无权调用垃圾回收器。下官只有上奏之权而无决策之权。 <br />(2) 程序员可以调用System.gc()，近通知JVM，并非运行垃圾回收器。**尽量少用**，会申请启动Full GC，成本高，影响系统性能。<br />(3) Object对象的finalize方法，是Java提供给程序员用来释放对象或资源的方法，**但是尽量少用**。
## this关键字
this的本质是当前对象的地址，是类里每一个普通方法的“隐式参数”，由系统自动传入方法。

- 普通方法中，this总是指向调用该方法的对象。
- 构造方法中，this总是指向正要初始化的对象。
- this()调用重载的构造方法，避免相同的初始化代码。但是只能在构造方法中使用，并且必须位于构造方法的第一句。
- this不能用于static方法中。
```java
/**
 * 测试this的用法
 * */
public class TestThis {
    int a,b,c;

    TestThis(){
        System.out.println("正要初始化对象："+this);
    }
    TestThis(int a, int b){
        // TestThis(); // 这样是无法调用构造方法的！
        this(); // 调用无参的构造方法，并且必须位于第一行！
        a = a; // 这里都是指的局部变量而不是成员变量
        this.a = a; // this.a才是对象里的a
        this.b = b;
    }

    TestThis(int a, int b, int c){
        this(a,b);
        this.c = c;
    }
    void sing(){

    }
    void eat(){
        System.out.println("当前对象："+this);
        this.sing(); // 调用本类中的sing();
        System.out.println("回家干饭！");
    }

    public static void main(String[] args) {
        TestThis hi = new TestThis(2,3);
        hi.eat();
    }

}

```
:::info
运行结果：<br />正要初始化对象：TestThis@723279cf<br />当前对象：TestThis@723279cf<br />回家干饭！
:::
## static关键字
**(1) 生命周期与类相同，在整个程序执行期间有效。**有如下特点：

- static属性和方法属于类，是公用变量，被所有实例共享，在类载入时进行初始化，而普通属性和方法属于对象。
- static成员变量只有一份。
- 一般使用“类名.类属性/方法”来调用。
- 在static方法中不可直接访问非static的成员。
```java
public class TestStatic {
    int id;
    String name;

    static String company = "字节跳动";
    public TestStatic(int id, String name){
        this.id = id;
        this.name = name;
    }

    public void login(){
        System.out.println(name);
    }

    public static void printCompany(){
        // login(); // 调用非静态成员变量，编译就会报错。
        System.out.println(company);
    }

    public static void main(String[] args) {
        TestStatic u = new TestStatic(101,"LISHENG");
        TestStatic.printCompany();
        TestStatic.company = "中科星图";
        TestStatic.printCompany();
        u.login();
        u.printCompany(); // Static member 'TestStatic.printCompany()' accessed via instance reference 
    }
}

```
:::info
运行结果：<br />字节跳动<br />中科星图<br />LISHENG<br />中科星图
:::
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699437269962-164b147b-5a00-43dd-bf0d-983e24dd6d7e.png#averageHue=%23caf8a2&clientId=uceabd04f-515f-4&from=paste&height=302&id=u9fbcef4b&originHeight=567&originWidth=1676&originalType=binary&ratio=2.25&rotation=0&showTitle=false&size=464565&status=done&style=none&taskId=uca5cc876-3569-4e7e-864d-829857dc91f&title=&width=893.8666666666667)<br />(2) 静态初始化块。<br />构造方法用于对象的普通属性的初始化操作。<br />静态初始化块，用于类的静态属性的初始化操作。<br />在静态初始化块中，不能直接访问非static成员。
```java
static String company;
static {
    System.out.println("执行类的初始化工作");
    company = "字节跳动";
    printCompany();
}
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699438854620-25446d77-00db-413a-b356-c1cde8f1b254.png#averageHue=%23e4e4e3&clientId=uceabd04f-515f-4&from=paste&height=182&id=u558d3cb5&originHeight=342&originWidth=1580&originalType=binary&ratio=2.25&rotation=0&showTitle=false&size=325567&status=done&style=none&taskId=ucdc20e1f-7803-40a0-9238-5a89e425c73&title=&width=842.6666666666666)
## 变量地分类和作用域
![image.png](https://cdn.nlark.com/yuque/0/2023/png/40430862/1699439131978-2a71da6a-5f09-42c2-8fb0-b27920dcef9d.png#averageHue=%23a5f7a0&clientId=uceabd04f-515f-4&from=paste&height=317&id=uf671d38b&originHeight=594&originWidth=859&originalType=binary&ratio=2.25&rotation=0&showTitle=false&size=248612&status=done&style=none&taskId=ua09dd06f-4dd8-4071-838d-4740aa79693&title=&width=458.1333333333333)<br />局部变量属于方法。成员变量属于对象。静态变量属于类。
