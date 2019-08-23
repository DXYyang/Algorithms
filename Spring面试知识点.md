# Spring面试知识点

- IOC:(控制反转) 应用本身不负责依赖对象的创建和维护，依赖对象的创建和维护是由外部容器负责的，这样控制权就由应用转移到了外部容器，控制权的转移即为反转。
- DI:(依赖注入) 所谓的依赖注入是指在运行期间，由外部容器动态地将依赖对象注入到组件中。
- AOP:(面向切面编程) 能够将那些与业务无关，却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可拓展性和可维护性。


## AOP
### AOP是基于代理模式实现的。
### Spring AOP的概念有：通知(Advice)、切点(Pointcut)和切面(Aspect) 
5类通知：

- 前置通知 (Before)：在目标方法执行前，执行通知
- 后置通知 (After)：在目标方法执行后，执行通知，不关心目标方法的返回结果是什么
- 返回通知 (After-returning):在目标方法执行后，执行通知
- 异常通知 (After-throwing）:在目标方法抛出异常后执行通知
- 环绕通知 (Around)：目标方法被通知包裹，通知在目标方法执行前和执行后都会被调用

切点(Pointcut)
如果说通知定义了在何时执行通知，那么切点定义了在何处执行通知。所以切点的作用就是通过匹配规则查找合适的连接点(Jointpoint)

切面(Aspect)
切面包含了通知和切点，通知和切点共同定义了切面是什么，在何时，何处执行切面逻辑

Spring AOP就是基于动态代理的，如果要代理的对象，实现了某个接口，那么Spring AOP会使用JDK Proxy，去创建代理对象，而对于没有实现接口的对象，就无法使用 JDK Proxy 去进行代理了，这时候Spring AOP会使用Cglib ，这时候Spring AOP会使用 Cglib 生成一个被代理对象的子类来作为代理，(也可以使用ASPECTJ)如下图所示：

![](./picture/AOP.jpg)

## Spring AOP 和 AspectJ AOP 有什么区别？
Spring AOP 属于运行时增强，而 AspectJ 是编译时增强。 Spring AOP 基于代理(Proxying)，而 AspectJ 基于字节码操作(Bytecode Manipulation)。

## Spring 中的 bean 的作用域有哪些?
- singleton : 唯一 bean 实例，Spring 中的 bean 默认都是单例的。
- prototype : 每次请求都会创建一个新的 bean 实例。
- request : 每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP request内有效。
- session : 每一次HTTP请求都会产生一个新的 bean，该bean仅在当前 HTTP session 内有效。
- global-session： 全局session作用域，仅仅在基于portlet的web应用中才有意义，Spring5已经没有了。Portlet是能够生成语义代码(例如：HTML)片段的小型Java Web插件。它们基于portlet容器，可以像servlet一样处理HTTP请求。但是，与 servlet 不同，每个 portlet 都有不同的会话

## SpringMVC 工作原理了解吗?
![](./picture/SpringMVC.jpg)
## Spring 框架中用到了哪些设计模式？
- 工厂设计模式 : Spring使用工厂模式通过 BeanFactory、ApplicationContext 创建 bean 对象。
- 代理设计模式 : Spring AOP 功能的实现。
- 单例设计模式 : Spring 中的 Bean 默认都是单例的。
-模板方法模式 : Spring 中 jdbcTemplate、hibernateTemplate 等以 Template 结尾的 - 对数据库操作的类，它们就使用到了模板模式。
- 包装器设计模式 : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
- 观察者模式: Spring 事件驱动模型就是观察者模式很经典的一个应用。
- 适配器模式 :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配Controller。

[SpringMVC设计模式](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485303&idx=1&sn=9e4626a1e3f001f9b0d84a6fa0cff04a&chksm=cea248bcf9d5c1aaf48b67cc52bac74eb29d6037848d6cf213b0e5466f2d1fda970db700ba41&token=255050878&lang=zh_CN#rd)
## @Component 和 @Bean 的区别是什么？
作用对象不同: @Component 注解作用于类，而@Bean注解作用于方法。
## 将一个类声明为Spring的 bean 的注解有哪些?
一般使用 @Autowired 注解自动装配 bean（@Qualifier 匹配相关bean名称，默认名称是类名首字母小写，如直接@Autowired装配，直接去找被注释的类或接口），要想把类标识成可用于 @Autowired 注解自动装配的 bean 的类,采用以下注解可实现：

- @Component ：通用的注解，可标注任意类为 Spring 组件。如果一个Bean不知道属于哪个层，可以使用@Component 注解标注。
- @Repository : 对应持久层即 Dao 层，主要用于数据库相关操作。
- @Service : 对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao层。
- @Controller : 对应 Spring MVC 控制层，主要用户接受用户请求并调用 Service 层返回数据给前端页面。
## Spring 事务中的隔离级别有哪几种?
**TransactionDefinition** 接口中定义了五个表示隔离级别的常量：

- **TransactionDefinition.ISOLATION\_DEFAULT**: 使用后端数据库默认的隔离级别，Mysql 默认采用的 REPEATABLE\_READ隔离级别 Oracle 默认采用的 READ\_COMMITTED隔离级别.
- **TransactionDefinition.ISOLATION\_READ\_UNCOMMITTED**: 最低的隔离级别，允许读取尚未提交的数据变更，可能会导致脏读、幻读或不可重复读
- **TransactionDefinition.ISOLATION\_READ\_COMMITTED**: 允许读取并发事务已经提交的数据，可以阻止脏读，但是幻读或不可重复读仍有可能发生
- **TransactionDefinition.ISOLATION\_REPEATABLE\_READ**: 对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，可以阻止脏读和不可重复读，但幻读仍有可能发生。
- **TransactionDefinition.ISOLATION\_SERIALIZABLE**: 最高的隔离级别，完全服从ACID的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，该级别可以防止脏读、不可重复读以及幻读。但是这将严重影响程序的性能。通常情况下也不会用到该级别。

## Spring 事务中哪几种事务传播行为?
**支持当前事务的情况**：

- **TransactionDefinition.PROPAGATION\_REQUIRED**： 如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务。
- **TransactionDefinition.PROPAGATION\_SUPPORTS**： 如果当前存在事务，则加入该事务；如果当前没有事务，则以非事务的方式继续运行。
- **TransactionDefinition.PROPAGATION\_MANDATORY**： 如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。（mandatory：强制性）

**不支持当前事务的情况**：

- **TransactionDefinition.PROPAGATION\_REQUIRES\_NEW**： 创建一个新的事务，如果当前存在事务，则把当前事务挂起。
- **TransactionDefinition.PROPAGATION\_NOT\_SUPPORTED**： 以非事务方式运行，如果当前存在事务，则把当前事务挂起。
- **TransactionDefinition.PROPAGATION\_NEVER**： 以非事务方式运行，如果当前存在事务，则抛出异常。

**其他情况**：

- **TransactionDefinition.PROPAGATION\_NESTED**： 如果当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行；如果当前没有事务，则该取值等价于**TransactionDefinition.PROPAGATION\_REQUIRED**。

## 简单实现Spring IOC的步骤:

Spring IOC的初始化过程:通过parseBeanDefinitionElement将XML的元素解析为BeanDefinition,然后存储在BeanDefinitionHolder中,最后将BeanDefinition对象注册为BeanFactory

1. 加载xml配置文件，遍历其中的标签
2. 获取标签中的id和class属性，加载class属性对应的类，并创建bean
3. 遍历标签中的标签，获取属性值，并将属性值填充到bean中
4. 将bean注册到bean容器中 

</br>[1、简单的IOC和AOP实现](http://www.tianxiaobo.com/2018/01/18/%E8%87%AA%E5%B7%B1%E5%8A%A8%E6%89%8B%E5%AE%9E%E7%8E%B0%E7%9A%84-Spring-IOC-%E5%92%8C-AOP-%E4%B8%8A%E7%AF%87/)

[2、简单的IOC和AOP实现](http://www.tianxiaobo.com/2018/01/18/%E8%87%AA%E5%B7%B1%E5%8A%A8%E6%89%8B%E5%AE%9E%E7%8E%B0%E7%9A%84-Spring-IOC-%E5%92%8C-AOP-%E4%B8%8B%E7%AF%87/)