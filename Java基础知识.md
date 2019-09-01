# Java基础类型

## 一、数据类型
## 包装类型
基本类型都有对应的包装类型，基本类型与其对应的包装类型之间的赋值使用自动装箱与拆箱完成

	Integer x=2 //装箱 调用了 Integer.valueOf(2)
	int y=x //拆箱 调用了 X.intValue()
## 缓存池
在 Java 8中, Integer缓存池的大小默认为-128-127
	
	Integer x = new Integer(123);
	Integer y = new Integer(123);
	System.out.println(x == y); // false 因为指向的两个不同的对象
	Integer z = Integer.valueof(123)=123;
	Integer k = Integer.valueof(123)=123;
	System.out.println( z==k );//true 因为123在缓存池内，所以指向的是同一内存。

valueOf()方法的实现比较简单，就是先判断值是否在缓存池中，如果在的话就直接返回缓存池的内容。

基本类型对应的缓冲池如下

- boolean values true and false
- all byte values
- short values between -128 and 127
- int values between -128 and 127
- char in the range \u0000 to \u007F

## String，StringBuffer and StringBuilder

### 1、可变性
- String不可变
- StringBuffer 和 StringBuilder可变

### 2、线程安全

- String不可变，因此是线程安全的
- StringBuilder不是线程安全的
- StringBuffer是线程安全的，内部使用synchronized进行同步
#
	String s1 = new String("aaa");
	String s2 = new String("aaa");
	System.out.println(s1==s2);//false
	String s3 = s1.intern();//获取s1的引用
	String s4 = s1.intern();
	System.out.println(s3==s4);//true
	String s5 = "bbb";
	String s6 = "bbb";
	System.out.println(s5==s6);//true

## float与double
Java不能隐式执行向下转型
形如1.1字面量是属于double类型，1.1f才是float类型
	
	//float f = 1.1
	float f = 1.1f
## 隐式类型转换
	short s1=1
	// s1 = s1 +1 因为字面量是int类型，而s1是short类型
	s1+=1; s1++; 使用+=或者++运算符可以执行隐式类型转换

## 参数传递
Java的参数是以值传递的形式传入方法中的，而不是引用传递。（相当于拷贝了一个副本）

## 二、面向对象
Java中有三个访问权限修饰符：private、protected以及public，如果不加访问修饰符，表示包级可见。 protected用于修饰成员，表示在继承体系中成员对于子类可见，但该修饰符对于类没有意义。

## 抽象类与接口
### 1、抽象类
抽象类和抽象方法都是使用abstract关键字进行声明的。如果一个类中包含抽象方法，那么这个类必须声明为抽象类。

抽象类与普通类的最大区别在于，抽象类不能被实例化，需要继承抽象类才能实例化其子类。

### 2、接口
接口不用实现定义的方法，但从Java8开始，接口也可以拥有默认的方法实现。

接口的成员(字段+方法)默认都是public的，并且不允许定义为private或者protected。

接口的字段默认都是static和final的。

### 两者的比较与使用选择
一个类可以实现多个接口，但是不能继承多个抽象类。
### 使用接口
- 需要让不相关的类都实现一个方法
- 需要使用多重继承
### 使用抽象类
- 需要在几个相关的类中共享代码
- 需要能控制继承来的成员的访问权限，而不都为public
- 需要继承非静态和非常量字段

## 重写与重载

### 重写（Override）
重写有三个限制:

- 子类方法的访问权限必须大于等于父类方法;
- 子类方法的返回类型必须是父类方法的返回类型或者为其子类型;
- 子类方法抛出的异常类型必须是父类抛出异常类型或为其子类型;

在调用一个方法时，先从本类中查找是否有对应的方法，如果没有查找到再到父类中查看，看是否有继承来的方法。否则，如果传递的参数是一个对象的话，就要对参数进行转型，转成父类之后看是否有对应的方法

- this.func(this)
- super.func(this)
- this.func(super)
- super.func(super)

### 重载(Overload)
存在于同一个类中，指一个方法与已经存在的方法名称上相同，但是参数类型、个数、顺序至少有一个不同。 **如果只是返回值不同，其他都相同不算重载**

## ==与equals()
- 对于基本类型，==判断两个值是否相等，基本类型没有equals()方法
- 对于引用类型，==判断两个变量是否引用同一个对象，而equals()判断引用的对象是否等价。
- 实现了equals()方法的内容，看对象中的内容是否等价，没有实现则使用==判断
#
	Integer x = new Integer(1);
	Integer y = new Integer(1);
	System.out.println(x.equals(y)); //true
	System.out.println(x == y);//false

## hashCode()
hashCode()返回散列值，而equals()是用来判断两个对象是否等价。等价的两个对象散列值一定相同，但是散列值相同的两个对象不一定等价。
在覆盖equals()方法时应总是覆盖hashCode()方法，保证等价的两个对象散列值也相等。
## 浅拷贝与深拷贝
- 浅拷贝与深拷贝只是针对数组与对象，基本数据类型没有
- 浅拷贝只拷贝一层，深拷贝拷贝多层
## 三、关键字
## final
### 1、数据
- 对于基本类型,final使数值不变;
- 对于引用类型，final使引用不变，也就不能引用其他对象，但是被引用的对象本身是可以修改的
#
	final int x=1;
	//x=2; 不能被修改
	final A y = new A();
	y.a = 1
### 2、方法
- 声明方法不能被子类重写。
- private方法隐式地被指定为final，如果在子类中定义的方法和基类中的一个private方法签名相同，此时子类的方法不是重写基类方法，而是在子类中定义了一个新的方法。
### 3、类
- 声明类不允许被继承
## static
- 静态变量：类所有的实例都共享静态变量，可以直接使用类名来访问它
#
	public class A{
		private int x;
		private static int y;
}
- 静态方法：静态方法在类加载的时候就存在了，它不依赖于任何实例，所以静态方法必须有实现，也就是说它不能是抽象方法（只能访问所属类的静态字段和静态方法，方法中不能有this和super关键字）
#
	public class A{
		private static int x;
		private int y;
		public static void func1(){
			int a = x;
			//int b = y;
			//int b = this.y;
		}
	}
- 静态语句块：在类的初始化时运行一次
#
	public class A{
	 static{
		}	
	}
- 静态内部类：非静态内部类依赖于外部类的实例，而静态内部类不需要引用外部实例。静态内部类不能访问外部类的非静态的变量和方法。
#
	public class OuterClass{
		class InnerClass{
		}
		static class StaticInnerClass{
		}
		public static void main(String[] args){
			OutClass outclass = new OuterClass();
			InnerClass innerClass = outClass.new InnerClass();
			StaticInnerClass staticInnerClass = new StaticInnerClass();
		}
	}	
- 静态导包：导入类的静态变量和方法，并且引用时不用再指明ClassName
	import static com.xxx.ClassName.*
### 初始化顺序
静态变量和静态语句块优于实例变量和普通语句块，静态变量和静态语句块的初始化顺序取决于它们在代码中的顺序

	public static String staticField = "静态变量";
	static{
		System.out.println("静态语句块");
	}
	public String field = "实例变量";
	{
		System.out.println("普通语句块");
	}
	public InitialOrderTest(){
		System.out.println("构造函数");
	}
存在继承的情况下，初始化顺序为：

-	父类（静态变量、静态语句块）
-	子类（静态变量、静态语句块）
-	父类（实例变量、普通语句块）
-	父类（构造函数）
-	子类（实例变量、普通语句块）
-	子类（构造函数）	
## 4、反射
每个类都有一个Class对象，包含了与类有关的信息。当编译一个新类时，会产生一个同名的.class文件，该文件内容保存着Class对象。类加载相当于Class对象的加载。反射可以提供运行时的类信息，并且这个类可以在运行时才加载进来

Class和java.lang.reflect一起对反射提供了支持，java.lang.reflect类库主要包含了3个类：

- Field:可以使用get()和set()方法读取和修改Field对象关联的字段。
- Method:可以使用invoke()方法调用与Method对象关联的方法。
- Constructor:可以使用Constructor的newInstance()创建新的对象。

### 反射的优点
- 可扩展性
### 反射的缺点
- 性能开销:反射涉及到了动态类型的解析，所以JVM无法对这些代码进行优化
- 安全限制:使用反射技术要求程序必须在一个没有安全限制的环境中运行 
- 内部暴露:由于反射允许代码执行一些在正常情况下不被允许的操作(比如访问私有的属性和方法)，可能会导致代码功能失调并破坏可移植性。

## 5、异常
Throwable 可以用来表示任何可以作为异常抛出的类，分为两种：Error 和 Exception。其中Error用来表示JVM无法处理的错误，Exception分为两种：

- 受检异常:需要用try...catch... 语句捕获并进行处理，并且可以从异常中恢复;
- 非受检异常:是程序运行时错误，例如除0会引发Arithmetic Exception，此时程序崩溃并且无法恢复。
- RuntimeException 是不受检查异常的基类

![](./picture/error.png)

## Java与C++的区别
- Java是纯粹的面向对象语言，C++即支持面向对象又支持面向过程
- Java通过虚拟机实现跨平台性，但是C++依赖于特定的平台
- Java没有指针，C++有指针
- Java支持自动垃圾回收，C++需要手动回收
- Java不支持多重继承，C++支持

## JRK,JDK,JVM
- JVM:Java虚拟机
- JRE:Java运行时的环境。jvm的标准实现和Java的一些基本类库
- JDK:Java开发工具包,集成了jre和一些好用的小工具
- 三者关系 JDK>JRE>JVM



	
