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

###2、线程安全

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

在调用一个方法时，先从本类中查找是否有对应的方法，如果没有查找到再到父类中查看，看是否有继承来的方法。否则，如果传递的参数是一个对象的换，就要对参数进行转型，转成父类之后看是否有对应的方法

- this.func(this)
- super.func(this)
- this.func(super)
- super.func(super)

### 重载(Overload)
存在于同一个类中，指一个方法与已经存在的方法名称上相同，但是参数类型、个数、顺序至少有一个不同。 **如果只是返回值不同，其他都相同不算重载**



	
