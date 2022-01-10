# 快捷键

取消缩进: Shift + Tab

markdown代码快:  Ctrl + Shift + k

run: Ctrl + Shift + F10



# JAVA NOTE



## Java 基础

### 运算:u

```java
s+=1; //s=s+1
s*=i; //s=s*i
```



### 关键字

class, interface, enum, int, true, if, else, for...

### 保留字

byValue, const....

### 标识符

0-9, a-Z ...(就是value name。 不可以使用关键字，保留字，数字开头....)

类名，接口名首字母大写

### 循环

```java
for(;;) == while(true)
```

### 增强型for循环(foreach循环):

```java
for(int n:arr): System.out.println(n);	//快速遍历输出array
```

### If else 简写:

```java
max = a> b? a: b;
```

### 数组是作为对象来实现的:

```java
char[] charArray = {'a', 'A'};

int[] a;
a = new int[10];
```

### 2D Array:

```java
int[][] num = {{1,2},{3,4},{5,6}};
num.length; //row
num[0].length;//column
```

### 方法重载(overload):

方法名相同，参数列表不同（数据类型，数量皆可）

```java
public void max(int a, int b){}

public int max(int a, int b){} //不是重载
public void max(double a, double b){}//是重载
public void max(double a, double b, double c){}//是重载
public int max(int[] arr){} //是重载
```

### 方法重写(override)

1.有继承关系的子类中

2.方法名，参数列表以及返回值相同

3.方法(传入)参数名可以不同

```java
public class Animal {
    public void eat(int age){}
}

public class Dog extends Animal{
    public void eat(int mounth){}//方法(传入)参数名可以不同
}
```



### Main方法调用方法需要定义对象(Object)

### 实际开发中尽量减少主方法(Main)中的代码，把代码封装到其他方法内，主方法只写核心的业务逻辑

### 数组传值:

数组是对象,但是这个数组对象并不是从某个类实例化来的，而是由JVM直接创建的

```java
public void change(int[] arr){
    arr[0]=15
}
public static void main(String[] args) {
    ClassName cn = new ClassName();
    int[] num = {1,2,3};
    cn.change(num);
    //num = {15,2,3}
}
```

### 可变参数列表

可变参数列表作为方法参数的重载

```java
public void sum(int... n){//可以有无数个int输入
    int sum = 0;
    for(int i:n) sum = sum+i;
    return sum;
}

public void sum(int a,int... n){}//可变参数必须放在最后
```

### 文档注释

javadoc 命令生成文档

```java

/**
*@author Zeqian
*@version 1.0
*/
```

### 面向对象:

```java
public class Cat{
    //property
    String name;
    int age;
    //function
    public void eat(){}
    public void sleep(){}
}

public class CatTest{
    public static void main(String[] args){
        //initialize object
        Cat cat = new Cat();
        //function
        cat.eat();
        //property
        String catName = cat.name;
    }
}
```

### 单一职责原则（单一功能原则）:

一个类干只一件事，代码复用率高

### 对象实例化:

```java
Cat cat;//声明对象，在内存栈(stack)中开辟空间，不能直接使用
new Cat();//实例化，在堆(heap)中开辟空间
Cat cat = new Cat();//堆空间的内存地址存放进cat

Cat one = new Cat();
Cat two = one//one 和 two指向同一片区域
```

### 构造方法（构造函数,构造器,construction method）:

1.new的好搭档

2.构造方法与类同名且没有返回函数

3.只能在对象实例化的时候调用

4.没有指定构造方法时，系统自动添加无参构造

5.构造方法中调用其他构造方法只能是第一条语句

```java
public class Cat{
    //property
    String name;
    int ages;
    double weights
    //无参构造
    public Cat(){}
    //带参构造
    public Cat(String name, int ages, double weights){
        this();//带参构造调用同一类的无参构造,其他普通方法无法调用构造方法
        this.name = name;
        this.ages = ages;
        this.weights = weights;
    }
}
```

### 封装:

private: 方法只能在本类中访问, 子类也不可以访问

getter/setter

```java
public Cat(String name) {
    this.setName(name);
}
public String getName() {
    return name;
}
public void setName(String name) {
    this.name = name;
}



import imooc.Cat;

imooc.Cat cat = new imooc.Cat();//直接在代码里导入包。class:Cat,package:imooc

```

### static(静态成员，类成员):

1.static方法就是没有this的方法。在static方法内部不能调用非静态方法，反过来是可以的。而且可以在没有创建任何对象的前提下，仅仅通过类本身来调用static方法。这实际上正是static方法的主要用途。

2.方便在没有创建对象的情况下来进行调用（方法/变量）。

3.共用内存中同一块区域，该类中所有对象共享

```java
public static int price(){}

Cat one = new Cat();

one.price = 2000;//通过对象名访问
Cat.price = 2000;//静态方法访问,通过类名访问
```

```java
public void run(){
    eat();//成员方法中，可以直接访问类中静态成员
}
public static void eat(){
    //静态方法中，无法直接访问非静态成员(方法和属性)
    //静态方法中,不能使用this
    //通过对象实例化可以调用非静态成员
    Cat temp = new Cat();
    temp.run();
}

Cat one = new Cat();
one.eat();
Cat.eat();//类成员通过类名调用
```

### 代码快:

```java
Namepublic void run(){
    {
        System.out.println("普通代码块");
    }
}

```

```java
public class Cat{
    {
        //代码块在类中
        //创建对象时调用，优先于构造方法执行
        //可以有多个
        System.out.println("构造代码块");
    }
}
```

```java
public class Cat{
    static{
        //类加载时调用，优先于构造代码块
        System.out.println("静态代码块");
    }
}
```

### 访问修饰符

X:表示支持

| 访问修饰符 | 本类 | 同包 | 子类 | 其他 |
| ---------- | ---- | ---- | ---- | ---- |
| private    | X    |      |      |      |
| 默认       | X    | X    |      |      |
| protected  | X    | X    | X    |      |
| public     | X    | X    | X    | X    |

子类方法重写（override）的访问修饰符的访问范围需要大于等于父类的访问范围

### super

1.每一个类都是Object的子类

2.父类的构造不允许被继承和重写，但会影响子类对象的实例化

3.子类默认调用父类无参构造。父类没有无参构造，则编译错误

4.this, super都不能在静态方法中调用

5.this(), super()不能同时出现(都需要放在第一行)

```java
super.eat();
    
super(names, age, species);//调用父类带参构造方法

this();//同一个类的无参构造方法
```



### 对象加载顺序:

**父类静态成员**——》父类静态代码块——》**子类静态成员**——》子类静态代码块——》Object——》父类成员属性——》父类构造代码块——》**父类构造方法**——》子类成员属性——》子类构造代码块——》**子类构造方法**



### object

1.操作对象尽量避免空指针异常

```java
java.lang;//自动加载

Object.equals(Object obj);//两个引用是否指向同一块内存地址，与 == 一样,经常重写

String.equals(Object obj);//两个字符串的值
String s1 = new String("hello");
String s2 = new String("hello");
s1.equals(s2);//true
s1==s2;//false

@Override
public boolean equals(Object obj){
    if(obj==null) return false;
    Animal temp=(Animal)obj;//obj强转成Animal类型
    if(this.getName().equals(temp.getName()) && this.getAge().equals(temp.getAge())){
        return true;
    }else{
        return false;
    }
}
    
```

```java
//没有重写toString
System.out.println(d1.toString());//animal.Dog@2ff4acd0
System.out.println(d1);//animal.Dog@2ff4acd0
```



### final

1.final class:该类没有子类(public final class == final public class )

2.final fucntion():该方法不允许被子类重写

3.final variable:该变量不允许被重新赋值

4.构造方法，构造代码块可以给没有赋值的final赋值

5.final不能用于修饰构造方法

```java
public final int num;
{
    num = 10;//构造代码块
}
public Aniaml(){
    num=10;//构造方法
}


final Animal animal=new Animal("haha",1);
animla = new animal;//报错，不能修改引用
animal.name = "HUAHUA";//可以修改


public final static float pi = 3.14;//定义常量
public final static String URL="www.google.com"//配置信息
```



### 注解(@Override)

1.源码注解(@Override):编译后不存在

2.编译时注解:源码和编译成.class依然存在

3.运行时注解(@Autowired):运行阶段依然起作用

```JAVA
@Override
public void eat() {
    super.eat();
}
```



### 多态(polymorphism)

向上转型

```java
Animal one = new Animal();
//向上转型
Animal two = new Cat();
Animal three = new Dog();

one.eat();//Animal eat
two.eat();//Cat eat
three.eat();//Dog eat
two.run();//无法运行
```



向下转型，强制类型转换

```java
Cat cat  = (Cat)two;
cat.eat();//Cat eat
cat.run();//Cat run


Dog dog = (Dog)two;//报错，Cat不能转为Dog
```



**instanceof:**

```java
if(two instanceof Cat){//true
    Cat cat  = (Cat)two;
    cat.eat();
    cat.run();
}
```

```java
public void feed(Animal obj){
    if (obj instanceof Cat){
        Cat temp = (Cat)obj;
        temp.eat();
        temp.playBall();
    }else if(obj instanceof Dog){
        Dog temp = (Dog)obj;
        temp.eat();
        temp.sleep();
    }
}

//性能优化
public void feed(Animal obj){
    obj.eat();
    if (obj instanceof Cat){
        Cat temp = (Cat)obj;
        temp.playBall();
    }else if(obj instanceof Dog){
        Dog temp = (Dog)obj;
        temp.sleep();
    }
}
```

**静态方法：父类的静态方法无法被子类重写。若父类子类同时拥有同名的静态方法：**

```java
Animal two = new Cat();
two.say()://Animal say

Cat cat = (Cat)two;
cat.say();//Cat say
```



### 抽象类(abstract):

1.父类Animal可以被实例化，但在一些程序中没有意义，加上abstract使其无法被直接实例化

2.可以通过向上转型指向子类实例

```java
public abstract class Animal{}
abstract public class Animal{}//abstract,public 位置可以互换

Animal one = new Animal();//Animal为抽象类时报错

Animal two = new Cat();//可以通过向上转型指向子类实例
```

1.子类必须重写父类的抽象方法(子类为抽象类可以不用重写)

2.抽象方法没有方法体(只有声明，没有实现)

3.抽象方法用于提醒子类实现相应的方法

4.抽象方法必定在抽象类中，抽象方法中不一定要有抽象方法

```java
public abstract void eat();//抽象方法，没有方法体
```



### 接口(interface):

1.接口描述不同类型具有相似的行为特征，定义某一批类所需要遵守的规范

2.接口不关心这些类的内部数据，也不关心这些类里方法的实现细节，它只规定这些类里必须提供某些方法

3.当一个类实现接口时，需要实现接口中的所有抽象方法，否则需要将该类设置为抽象类

4.当一个类实现多个接口时，多个接口有重名变量时可能会报错。需通过(接口名.变量名)访问具体变量

```java
//接口访问修饰符：public, default,没有写默认为public
//接口中抽象方法可以不写abstract关键字

public interface INet{
    //jdk1.8 static,default
    //static:静态方法，可以带方法体。通过接口名调用而不是通过实例
    //不可以在实现类中重写，可以用接口名调用
    static void stop(){
        System.out.println("Halt");
    }
    
    //default:默认方法，可以带方法体
    //可以在实现类中重写，可以通过接口的引用调用
    default void connection(){
        System.out.println("Connecting");
    }
}


public interface Iphoto{
    int PI=3.14;//接口中可以包含常量，默认public static final
    			//Iphoto.PI使用
    
    public void photo();
    
}

public class Camera implements Iphoto{
    public void photo(){
        System.out.println("Camera photo");
    }
}

public class SmartPhone extends Phone implements Iphoto,INet{
    public void photo(){
        System.out.println("Phone photo");
    }
    
    public void connection(){
        Iphoto.super.connection();//调用接口中默认方法
        //Iphoto.connection(); 报错，接口名只能直接访问静态方法
    }
}


Iphoto ip = new SmartPhone();
ip.photo();//Phone photo
ip = new Camera();
ip.photo();//Camera photo
```

1.接口可以继承多个父接口

```java
public interface IFather{
    void say();
}
public interface IFather2{
    void fly();
}

public interface ISon extends IFather,IFather2{
    void run();
}
public class Demo implements ISon{
    @Override
    public void say(){
        
    }
    @Override
    public void fly(){
        
    }
    @Override
    public void run(){
        
    }
}
```



### 内部类:

1.**成员内部类：**#内部类在外部使用时，无法直接实例化，需要借助外部类信息才能完成实例化 #内部类可以直接访问外部类的成员，出现同名则优先访问内部类的定义 #可以使用 外部类.this.成员 访问外部类中的同名信息

```java
//成员内部类
public class Person {
    int age;
    public void eat(){}
    public Heart getHeart(){
        return new Heart();
    }
    class Heart{
        public String beat(){
            eat();
            return "heart beat";
        }
    }
}


//同包main
Person lily = new Person();
lily.age = 12;

Heart myHeart = new Heart();//报错，无法访问

//获取内部类对象实例方法1：new 外部类.new 内部类
Person.Heart myHeart = new Person().new Heart();
System.out.println(myHeart.beat());
//获取内部类对象实例方法2：外部类对象.new 内部类
myHeart = lily.new Heart();
//获取内部类对象实例方法3：外部类对象.获取方法
myHeart = lily.getHeart();
```

2.**静态内部类：**#只能直接访问外部类静态成员，非静态需通过对象实例调用 #静态内部类对象实例不依赖于外部类对象 #外部类.内部类.静态成员 访问内部类中的静态成员 

```java
//静态内部类
public class Person {
    int age;
    public void eat(){}
    public Heart getHeart(){
        return new Heart();
    }
    static class Heart{
        int age=10;
        public String beat(){
            new Person().eat();
            return new Person().age+" heart beat";
        }
    }
}

//同包main
Person lily = new Person();
lily.age = 12;

Person.Heart myHeart = new Person.Heart();
```

3.**方法内部类：**#定义在方法内部，作用范围也在方法内 

#class前不可以有public,private,protected,static #没有静态成员

```java
public Object getHeart(){
    
    class Heart{
        int age=10;
        public String beat(){
            new Person().eat();
            return new Person().age+" heart beat";
        }
    }
    return new Heart().beat();
}

Person lily = new Person();
lily.getHeart();
```

4.**匿名内部类：**#将类的定义与创建放到一起完成 #匿名内部类没有类型以及实例对象的名称 #无法添加访问修饰符#无法编写构造方法 #没有静态成员 #匿名内部类可以实现接口或者继承父类，但不可兼得

```java
public abstract class Person {
    private String name;
    public Person(){}
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public abstract void read();
}


PersonTest test = new PersonTest();
//匿名内部类
test.getRead(new Person(){
    {//构造代码块可以用来初始化属性}
    @Override
    public void read() {
        System.out.println("Man like read");
    }
});
```



## Java 常用工具类

### Java 异常:

Throwable:

​	--Error(VirtualMachineError, OutOfMemoryError, ThreadDeath): 无法解决,不用关心

​	--Exception(): 可处理

​		--Unchecked Exception(RuntimeException):编译器不要求强制处理

​			--NullPointerException, ArrayIndexOutOfBoundsException, ArithmeyicException, ClassCastException

​		--Checked Exception:编译器要求必须处理的异常

​			--IOException, SQLException



**捕获异常:** try, catch, finally

**声明异常:** throws

**抛出异常:** throw

try 后必须根一个catch或者finally

```java
try {
    Scanner scan = new Scanner(System.in);
    System.out.print("please input num one: ");
    int one = scan.nextInt();
    System.out.print("please input num two: ");
    int two = scan.nextInt();
    System.out.println("one/two: " + (one / two));
}catch (ArithmeticException e){
    System.out.println("DO NOT DIVIDE 0");
    e.printStackTrace();
}catch (InputMismatchException e){
    System.out.println("PLEASE INPUT INTEGER NUMBER");
    e.printStackTrace();
}catch (Exception e){ //catch一个Exception保证没有漏网之鱼，一定要放在最后面
    System.out.println("EXCEPTION!");
    e.printStackTrace();
    System.exit(17);//强行终止Java虚拟机，数值非0表示异常终止
}finally {
    System.out.println("DONE");
}
```

try, catch, finally 都含有return,只有finally里的return会执行



**throw & throws:** throws E1,E2,E3只是告诉程序这个方法可能会抛出这些异常，方法的调用者可能要处理这些异常，而这些异常E1，E2，E3可能是该函数体产生的。throw则是明确了这个地方要抛出这个异常。

```java
//throws
public static int test() throws ArithmeticException,InputMismatchException{//throws Exception，编译器会要求强制处理异常。如果是子类(ArithmeticException,InputMismatchException)则不会
    Scanner scan = new Scanner(System.in);

    System.out.print("please input num one: ");
    int one = scan.nextInt();
    System.out.print("please input num two: ");
    int two = scan.nextInt();

    System.out.println("DONE");
    return one/two;
}

//Main:
try {
    int result = test();
    System.out.println("one/two: " + result);
}catch (ArithmeticException e){
    System.out.println("DO NOT DIVIDE 0");
    e.printStackTrace();
}catch (InputMismatchException e){
    System.out.println("PLEASE INPUT AN INTEGER");
    e.printStackTrace();
}
```

**throw:** 只能抛出Throwable或其子类

```java
//throw
//1.通过try, catch包含throw语句--自己抛出自己处理
public static void testAge(){
    try {
        Scanner input = new Scanner(System.in);
        System.out.println("Input age");
        int age = input.nextInt();
        if(age<18 || age>80){
            throw new Exception("18 < age < 80");
        }else {
            System.out.println("Welcome to the hotel");
        }
    } catch (Exception e) {
        e.printStackTrace();
    }
}

//2.通过throws在方法声明出抛出异常类型--谁调谁处理，也可以继续向上抛给上层来处理
public static void testAge() throws Exception {//Throwable是Exception的父类，可以写在这
    Scanner input = new Scanner(System.in);
    System.out.println("Input age");
    int age = input.nextInt();
    if(age<18 || age>80){
        throw new Exception("18 < age < 80");
    }else {
        System.out.println("Welcome to the hotel");
    }
}
//main:
try {
    testAge();
} catch (Exception e) {
    e.printStackTrace();
}
```

**自定义异常:**

```java
public class HotelAgeException extends Exception{
    public HotelAgeException(){
        super("18 < age < 80: Form HotelAgeException Class");
    }
}


public class TryDemoFour {
    public static void main(String[] args) {
        try {
            testAge();
        } catch (HotelAgeException e) {
            System.out.println(e.getMessage());
        }
    }
    public static void testAge() throws HotelAgeException {
        Scanner input = new Scanner(System.in);
        System.out.println("Input age");
        int age = input.nextInt();
        if(age<18 || age>80){
            throw new HotelAgeException();
        }else {
            System.out.println("Welcome to the hotel");
        }
    }
}
```



### Java 包装类

**Float, Short, Integer**数值型包装类都继承自Number类

**Character, Boolean**直接继承自Object

**装箱:**

```java
//1.自动装箱
int t1 = 2;
Integer t2 = t1;

//2.手动装箱
Integer t3 = new Integer(t1);
```

**拆箱:**

```java
//1.自动拆箱
int t4 = t2;
//2.手动拆箱
int t5 = t2.intValue();
double t6 = t2.doubleValue();//可转换数据类型

//练习
Integer one = new Integer(100);
Integer two = new Integer(100);
System.out.println(one == two);//False

Integer three = 100;//Integer three = Integer.valueOf(100); 实际执行语句
System.out.println(three == 100);//True, three自动拆箱

Integer four = 100;//Integer four = Integer.valueOf(100); -128<参数<127则在对象池中直接产生
System.out.println(three == two);//True,three和four指向缓存(对象池)中的同一片区域
Integer five = 200;
System.out.println(five == 200);//True, five自动拆箱
Integer six = 200;//Integer six = new Integer(200);
System.out.println(five == six);//False, five和six无法直接产生于对象池，使用new

// float和double不会应用对象常量池
Double d1 = Double.valueOf(100);
System.out.println(d1 == 100);//True, d1自动拆箱
Double d2 = Double.valueOf(100);
System.out.println(d1 == d2);//False, double不会应用对象常量池
```

**基本数据类型与字符串转换:**

```java
int t1 = 2;
//int to String
String t2 = Integer.toString(t1);
//String to int
int t3 = Integer.parseInt(t2);
int t4 = Integer.valueOf(t2);
```





### String常用方法

**String 不可变: String对象一旦被创建，不可被修改。修改String本质上是创建了一个新的对象**

```java
//创建String对象的方法
String s1="Hello world";
String s2 = new String("Hello world");

System.out.println(s1.charAt(3));//l
System.out.println(s1.substring(4,7));//o w

System.out.println(s1.indexOf('o'));//4
System.out.println(s1.lastIndexOf('o'));//7
```



```java
//String与byte转换
byte[] arrs = s1.getBytes(StandardCharsets.UTF_8);
for (int i=0; i<arrs.length; i++){
    System.out.print(arrs[i]+" ");
}//72 101 108 108 111 32 119 111 114 108 100 

String s3 = new String(arrs);
System.out.println(s3);//Hello world
```



```java
String s1 = "Hello world";
String s2 = "Hello world";
String s3 = new String("Hello world");

System.out.println(s1==s2);//true, 常量池
System.out.println(s1.equals(s2));//true

System.out.println(s1==s3);//false, 地址不同
System.out.println(s1.equals(s3));//false
```

   

**StringBuilder:** 不同于String的不可变性，StringBuilder具有可变性

StringBuffer VS StringBuilder: 用法一样，StringBuilder性能略好但是线程不安全。单线程下基本使用StringBuilder

```java
StringBuilder str = new StringBuilder("Hello");
System.out.println(str.append(',').append("Yoo!"));//Hello,Yoo!
System.out.println(str);//Hello,Yoo!

System.out.println(str.delete(3,5));//Hel,Yoo!

System.out.println(str.insert(4,"INSERT"));//Hel,INSERTYoo!
System.out.println(str.replace(4,10,"REPLACE"));//Hel,REPLACEYoo!
```



### 集合

**Collection:** List(ArrayList), Queue(LinkedList) --(有序，重复)

​					Set(HashSet) --(无序，不重复)

**Map:** Map(HashMap)



```java
//ArrayList
List list = new ArrayList();
list.add("Java");
list.add("C");
list.add("C++");
list.add("Go");
list.add("swift");

System.out.println("# in the List is: " + list.size());//5

for (int i = 0; i<list.size(); i++){
    System.out.print(list.get(i)+ " ");
}//Java C C++ Go swift 

list.remove(2);//remove C++
list.remove("Java");//remove Java

for (int i = 0; i<list.size(); i++){
    System.out.print(list.get(i)+ " ");
}//C Go swift

//ArrayList store Obj
Notice notice1 = new Notice(1,"Welcome","Admin",new Date());
Notice notice2 = new Notice(2,"Due Date!!!","teacher",new Date());
Notice notice3 = new Notice(3,"Sign","teacher",new Date());

ArrayList noticeList = new ArrayList();
noticeList.add(notice1);
noticeList.add(notice2);
noticeList.add(notice3);

for (int i=0; i<noticeList.size();i++){
    System.out.println((i+1)+":"+((Notice)(noticeList.get(i))).getTitle());//noticeList.get(i)返回Object,需要强转成Notice
}
/*
1:Welcome
2:Due Date!!!
3:Sign
*/

Notice notice4 = new Notice(4,"GOGOGO","Admin",new Date());
noticeList.add(1,notice4);//指定位置增加
/*1:Welcome
2:GOGOGO
3:Due Date!!!
4:Sign
*/

notice4.setTitle("RUA");
noticeList.set(1,notice4);//指定位置修改
/*
1:Welcome
2:RUA
3:Due Date!!!
4:Sign
*/
```

```java
//HashSet();
//Iterator itr = set.iterator();

Set set = new HashSet();
set.add("blue");
set.add("red");
set.add("black");
set.add("yellow");
set.add("white");
set.add("white");//插入重复元素不会报错，但不会实际插入

System.out.print("Set: ");
Iterator itr = set.iterator();
while (itr.hasNext()){
    System.out.print(" "+itr.next());
}//Set:  red blue white black yellow

//HashSet store Obj
Cat huahua = new Cat("HuaHua",12,"BR");
Cat fanfan = new Cat("FanFan",3,"CN");

Set set = new HashSet();
set.add(huahua);
set.add(fanfan);

Iterator itr = set.iterator();
while (itr.hasNext()){
    System.out.println(itr.next().toString());
}
//Cat{name='FanFan', month=3, species='CN'}
//Cat{name='HuaHua', month=12, species='BR'}

Cat huahua01 = new Cat("HuaHua",12,"BR");
set.add(huahua01);
itr = set.iterator();
while (itr.hasNext()){
    System.out.println(itr.next().toString());
}
//Cat{name='FanFan', month=3, species='CN'}
//Cat{name='HuaHua', month=12, species='BR'}
//Cat{name='HuaHua', month=12, species='BR'}
//huahua01 与 huahua 值一样，但地址不一样所以可以重复。

//通过值是否相同来判断是否添加对象，需要重写两个方法:hashCode, equals
//Cat:可以通过自动生成来重写
@Override
public boolean equals(Object o) {
    if (this == o) return true;//同一个对象？
    if (!(o instanceof Cat)) return false;//同一个类？
    Cat cat = (Cat) o;
    return getMonth() == cat.getMonth() && Objects.equals(getName(), cat.getName()) && Objects.equals(getSpecies(), cat.getSpecies());
}

if (set.contains(huahua)) System.out.println("Find HuaHua");//Find HuaHua

//Find by name
itr = set.iterator();
boolean flag = false;
while (itr.hasNext()){
    Cat cat = (Cat)(itr.next());
    if (cat.getName().equals("HuaHua")) {
        flag=true;
        break;
    }
}
String info = flag? "Find HuaHua by name": "No HuaHua by name";
System.out.println(info);//HuaHua by name
```

```java
//泛型限制集合与迭代器中只能存放Cat
Set<Cat> set = new HashSet<Cat>();
Iterator<Cat> itr = set.iterator();

while (itr.hasNext()){
    cat =itr.next();//无需强制转换成Cat
    if (cat.getName().equals("HuaHua")) {
        flag=true;
        break;
    }
}

//删除集合中的元素
for (Cat c : set){
    if (c.getName().equals("FanFan")){
        set.remove(c);
        break;//集合读取数据中禁止对数据进行删除，这里加break是为了删除数据后停止读取数据
    }
}
for (Cat c : set) System.out.println(c);
//Cat{name='KK', month=3, species='CN'}
//Cat{name='FanFan', month=3, species='CN'}
System.out.println(set.isEmpty());//false
```

```java
//Map
//key-value键值对
//HashMap()基于哈希表实现的接口，允许使用null值和键，key值不允许重复
//Entry对象无序排列
//Interface Map<K,V>
Map<String,String> animal = new HashMap<String,String>();
System.out.println("Please entry 3 pair K,V");
Scanner scan = new Scanner(System.in);
int i = 0;
while (i<3){
    System.out.println("Entry K");
    String key = scan.next();
    System.out.println("Entry V");
    String value = scan.next();
    animal.put(key, value);
    i++;
}//input cat, dog , apple
System.out.println("*********************");
System.out.println("Output all values");
Iterator<String> iter = animal.values().iterator();
while (iter.hasNext()){
    System.out.print(iter.next()+" ");
}//out apple dog mice -->无序，首字母排序输出

//通过entrySet()输出
System.out.println("*********************");
System.out.println("entrySet: ");
Set<Entry<String,String>> entrySet = animal.entrySet();
for (Entry<String,String> entry:entrySet){
    System.out.println(entry.getKey()+"-"+entry.getValue());
}
//dogK-dogV
//appleK-appleV
//catK-catV

//Search:
System.out.println("Search Key");
String strSearch = scan.next();//catK
//get keySet
Set<String> keySet = animal.keySet();
for (String key:keySet){
    if (strSearch.equals(key)){
        System.out.printf("Find it!!!"+key+"-"+animal.get(key));
        break;
    }
}//Find it!!!catK-catV
```



### 泛型:



```java
public void sellGoods(List<? extends Goods> goods){
    //<? extends Goods> --> Goods子类都可以传进来
    for (Goods g:goods){
        g.sell();
    }
}
//mauin:
List<Book> book = new ArrayList<>();
book.add(new Book());
book.add(new Book());
List<Clothes> clothes = new ArrayList<>();
clothes.add(new Clothes());
clothes.add(new Clothes());
List<Shoes> shoes = new ArrayList<>();
shoes.add(new Shoes());
shoes.add(new Shoes());

GoodsSeller goodsSeller = new GoodsSeller();
goodsSeller.sellGoods(book);
```

自定义泛型:

```java
//数据类型参数化
public class NumGeneric<T> {
    private T num;

    public T getNum() {
        return num;
    }
    public void setNum(T num) {
        this.num = num;
    }
    
    public static void main(String[] args) {
        NumGeneric<Integer> intNum = new NumGeneric<>();
        intNum.setNum(10);
        System.out.println("Integer:" + intNum.getNum());//10

        NumGeneric<Float> flotNum = new NumGeneric<>();
        flotNum.setNum(10.1f);
        System.out.println("Float:" + flotNum.getNum());//10.1
    }
}
```

```java
//双参
public class TwoNumGeneric<T,X> {
    private T num1;
    private X num2;

    public void genNum(T num1,X num2){
        this.num1 = num1;
        this.num2 = num2;
    }
    public T getNum1() {
        return num1;
    }
    public void setNum1(T num1) {
        this.num1 = num1;
    }
    public X getNum2() {
        return num2;
    }
    public void setNum2(X num2) {
        this.num2 = num2;
    }

    public static void main(String[] args) {
        TwoNumGeneric<Integer, Float> numObj = new TwoNumGeneric<>();
        numObj.genNum(25,5.0f);
        System.out.println("num1="+numObj.getNum1()+" num2="+numObj.getNum2());//num1=25 num2=5.0
    }
}
```

泛型方法不一定在泛型类中

```java
public class GenericMethod {
    public <T> void printValue(T t){
        System.out.println(t);
    }

    public static void main(String[] args) {
        GenericMethod gm = new GenericMethod();
        gm.printValue(10);//10
        gm.printValue("hello");//hello
        gm.printValue(false);//false
    }
}
//加限定:
public class GenericMethod {
    public <T extends Number> void printValue(T t){
        System.out.println(t);
    }

    public static void main(String[] args) {
        GenericMethod gm = new GenericMethod();
        gm.printValue(10);//10
        gm.printValue("hello");//报错XXX
        gm.printValue(false);//报错XXX
    }
}
```

### 多线程：

*创建一个Thread类，或其子类对象

*创建一个实现Runnable接口的类对象

```java

```









## 设计模式

### 单列模式:

**优点：内存中只有一个对象(节省内存)，避免频繁创建销毁对象(提升性能)，避免对共享资源的多重占用**

**缺点：扩展困难，对象长期不利用会被系统默认为垃圾回收(对象状态丢失)**

**使用场景：创建对象占用资源过多，平凡用到该对象**

​					**对系统内存资源要求统一读写，如读写配置信息**

​					**多个实例存在会引起程序逻辑错误，如号码生成器**



1.一个类有且只有一个实例

2.类中有创建实例的方法

3.向整个系统提供这个实例

```java
//只提供私有的构造方法
//含有一个该类的静态私有对象(static)
//提供一个公有的静态方法用于创建，获取静态私有对象

//饿汉式：对象创建过程中实例化
//空间换时间
public class SingletonOne {
    //1.创建类中私有构造
    private SingletonOne(){
    }
    //2.创建该类型中的私有静态实例
    private static SingletonOne instance = new SingletonOne();
    //3.创建公有静态方法，返回静态实例对象
    public static SingletonOne getInstance(){
        return instance;
    }
}

public class Test {
    public static void main(String[] args) {
        SingletonOne one = SingletonOne.getInstance();
        SingletonOne two = SingletonOne.getInstance();
        System.out.println(one==two);//True
    }
}

//懒汉式：静态公有方法中实例化
//时间换空间
//类内实现实例对象创建时并不直接初始化，直到第一次调用get方法时，才完成初始化的操作
public class SingletonTwo {
    //1.创建类中私有构造
    private SingletonTwo(){
    }
    //2.创建静态的该类实例对象
    private static SingletonTwo instance = null;
    //3.创建开放的静态方法，提供实例对象
    public static SingletonTwo getInstance(){
        if(instance==null) instance=new SingletonTwo();
        return instance;
    }
}
```

**饿汉vs懒汉**

**饿汉:线程安全**

**懒汉:线程风险**

