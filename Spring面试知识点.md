#Spring面试知识点

- IOC:(控制反转) 应用本身不负责依赖对象的创建和维护，依赖对象的创建和维护是由外部容器负责的，这样控制权就由应用转移到了外部容器，控制权的转移即为反转。
- DI:(依赖注入) 所谓的依赖注入是指在运行期间，由外部容器动态地将依赖对象注入到组件中。
- AOP:(面向切面编程) 用来在系统中提升业务的分离，把日志、安全、事务等东西和核心业务分离开来，甚至核心业务都不知道它们的存在。基本实现就是对相关方法进行拦截，添加所需的动作。

##Spring IOC的初始化过程:
通过parseBeanDefinitionElement将XML的元素解析为BeanDefinition,然后存储在BeanDefinitionHolder中,最后将BeanDefinition对象注册为BeanFactory
##简单实现Spring IOC的步骤:
1. 加载xml配置文件，遍历其中的标签
2. 获取标签中的id和class属性，加载class属性对应的类，并创建bean
3. 遍历标签中的标签，获取属性值，并将属性值填充到bean中
4. 将bean注册到bean容器中 
##简单的AOP实现：
###AOP是基于代理模式实现的。
###Spring AOP的概念有：通知(Advice)、切点(Pointcut)和切面(Aspect) 
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

</br>[1、简单的IOC和AOP实现](http://www.tianxiaobo.com/2018/01/18/%E8%87%AA%E5%B7%B1%E5%8A%A8%E6%89%8B%E5%AE%9E%E7%8E%B0%E7%9A%84-Spring-IOC-%E5%92%8C-AOP-%E4%B8%8A%E7%AF%87/)

[2、简单的IOC和AOP实现](http://www.tianxiaobo.com/2018/01/18/%E8%87%AA%E5%B7%B1%E5%8A%A8%E6%89%8B%E5%AE%9E%E7%8E%B0%E7%9A%84-Spring-IOC-%E5%92%8C-AOP-%E4%B8%8B%E7%AF%87/)