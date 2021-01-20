# Spring基础原理

spring核心容器：

+ BeanFactory: 负责初始化各种Bean 并调用他们的生命周期方法

  ```java
  //不常用
  BeanFactory beanfactory = new XmlBeanFactory(new FileSystemResource("D:/applicationContext.ml"))
  ```

  

+ ApplicationContext: BeanFactory的子接口：ApplicationContext也叫应用上下文。

  ```java
  1、通过 ClassPathXmlApplicationContext 创建
      ApplicationContext applicationContext = new ClassPathXmlApplicationCo text(String 		configLocation);
      //configLocation 配置文件的名称和位置（相对类的路径）
      
  2、通过 FileSystemXmlApplicationContext 创建
  ApplicationContext applicationContext = 
  new FileSystemXmlApplicationContext(String configLocation);
  //configLocation 绝对路径
  ```

+ web服务器实例化ApplicationContext容器

  ```xml
  <!… 指定 Spring 配置文件的位置，多个配置文件时，以逗号分隔一〉
  <context-param> 
      <param-name>contextConfigLocation<!param-name> 
      <!一 Spring 将加载 spring 目录下的 applicationContext .xml 文件一
      <param-value> 
      	classpath:spring/applicationContext.xml 
      </param-value> 
  </context-param> 
  <!一指定以 ContextLoaderListener 方式启动 Spring 容器
  <listener> 
      <listener-class> 
      	org.springframework.web.context.ContextLoaderListener
      </listener-class> 
  </listener>
  ```

  

+ Spring获取Bean实例

+ ```java
  1、
  Object getBean(String name): 根据容器中 Bean id name 来获取指定的 Bean ，获
  取之后需要进行强制类型转换
  2、
  <T> T getBean(Class<T> requiredType) 根据类的类型来获取 Bean 的实例 由于此方
  法为泛型方法，因此在获取 Bean 之后不需要进行强制类型转换
  ```

  

+ 实际开发中多使用ApplicationContext

### 1.3 Spring 入门程序

+ Bean的Xml注入，

```xml
<?xml version="l.O" encoding="UTF-8"?> 
<beans xmlns="http://www.springframework.org/schema/beans " 
xmlns : xsi="http://www.w3.org/2001/XMLSchema-instance " 
xsi :schemaLocation="http://www . springframework.org/schema/beans 
http : //www .springframework . org/schema/beans/spring-beans-4 . 3 . xsd"> 
<!一将指定类配置给 Spring ，让 Spring 创建其对象的实例一>
<bean id="userDao" c1ass="com.itheima.ioc.UserDaoII 1" /> 
</beans>
```

```java
public class TestloC {
public static void main(String[] args) {
    / /1.初始化 spring 容器，加载配置文件
    ApplicationContext applicatio Cb text = 
    new ClassPathXmlApplicationContext( "applicationContext . xml " ); 
    //2 通过容器获取 userDao 实例
    UserDao userDao = (UserDao) app1icationContext . getBean("userDao") ; 
    //3 调用实例巾的 say ()方法
    userDao .say();
    }
}
```



#### 1.4 依赖注入

+ 概念：

  + 依赖注入：Spring 容器的角度来看， Spring 容器负责将被依赖对象赋值给调用者的成员变量，这相

    当于为调用者注入了它依赖的实例，这就是 Spring 的依赖注入.

  + 控制反转：对象的实例不再由调用者来创建，而是由 Spring 容器来创建，

    Spring 容器会负责控制程序之间的关系，而不是由调用者的程序代码直接控制这样，控制权

    由应用代码转移到了 Spring 容器，控制权发生了反转，这就是 Spring 的控制反转

  + 他们两个是一个概念 不过是从不同的角度看待问题的

+ 依赖注入的实现方式

  + 属性Setter方法注入：屌用无参构造器或无参静态工厂实例化Bean后，调用Bean的Setter方法，即可实现基于Setter方法的注入
  + 构造方法注入：调用带参数的构造方法来实现

  ```xml
  <!一添加一个 id userService 的实例…〉
  <bean id= "u se ervice class= co itheima.ioc .U serServicelmpl">
      <!一将 id userDao Bean 实例注入到 userService 实例中一〉
      <property name="userDao" ref="userDao" />   ## 第一个userdao是属性名 第二个是另一个Bean名字
  </bean〉
  ```

  