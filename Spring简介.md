# Spring简介

##### 1、spring是一个轻量级的框架

##### 2、spring核心主要两部份
- aop:面向切面编程，扩展功能不是修改源代码实现
- ioc:控制反转 -把对象的创建不是通过new方式实现，而是交给spring配置创建类对象


##### 3、spring是一站式框架
spring在javaee三层结构中，每一层都提供不同的解决技术

- web层：springMVC
- service层：spring的ioc
- dao 层：spring的jdbcTemlate

##### 4、spring版本
- hibernate5.x
- spring4.x
- 

---
# Spring的ioc操作

##### 1、把对象的创建交给spring进行管理

##### 2、ioc操作的两部分
- ioc的配置文件方式
- ioc的注解方式


---
# IOC底层原理
1、ioc底层原理使用的技术
- xml配置文件
- dom4j解决xml
- 工厂设计模式、
- 反射

> [IOC原理实现过程](http://note.youdao.com/noteshare?id=876daedc6d1b66d4af6164f2e609766f)


---

# IOC入门案例
- 创建在src文件夹下applicationContenxt.xml配置文件
- 添加schema

    applicationContenxt.xml
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="user" class="com.wj.pojo.User"/>
    </beans>
    ```
    
    ```
    //加载spring配置文件
    ApplicationContext applicationContext=
            new ClassPathXmlApplicationContext("applicationContext.xml");
    //得到配置创建的对象
    User user= (User) applicationContext.getBean("user");
    ```

---
# Spring的bean管理(XML)
##### 1、在Spring里面通过配置文件创建对象

##### 2、Bean实例化方式
- 使用类的参数构造函数创建(重点)
    ```
    <bean id="user" class="com.wj.pojo.User"/>
    ```
- 使用静态工厂创建
    
    ```
    1、创建静态的方法，返回类的对象
    ```
   
    ```
    public class Factroy{
        public static User getUser(){
            return new User();
        }
    }
    <bean id="user" class="com.wj.pojo.Factory" factory-method="getUser"/>
    ```

- 使用实例工厂创建
    ```
    1、创建非静态的方法，返回类的对象
    ```
    ```
    public class Factroy{
        public User getUser(){
            return new User();
        }
    }
    <bean id="factroy" class="com.wj.Factroy"/>
    <bean id="user" factory-bean="factroy" factory-method="getUser"/>
    ```
##### 3、Bean标签常用属性
- id属性
    ```
    起名称，id属性名称任意命名但不能包含特殊符号。
    根据ID的值获取类的对象
    ```
- class属性
    ```
    创建对象所在类的全路径。
    ```
- name属性
    ```
    功能和id属性是一样的
    但name属性值可以包含特殊符号
    现已不太常用
    ```
- scope属性
    ```
    Bean的作用范围
    
    singleton:默认值，单利
    prototype:多例
    request:WEB项目中，Spring创建一个Bean的对象，将对象存入到request域中
    session:WEB项目中，Spring创建一个Bean的对象，将对象存入到session域中
    globalSession:WEB项目中，应用在porlet环境，如果没有porlet环境那么globalSession相当于session
    ```
    
##### 4、属性注入

```
创建对象的时候，向类里面的属性设置值
```




