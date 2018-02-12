---
date: 2018-01-16 17:53
status: public
title: 'Spring IOC 底层原理'
---

> 什么是IOC控制反转

专业术语就是将创建对象的权力交给第三方框架去处理。
> 没学Spring框架之前用到的技术

没学Spring之前，在做jsp的项目的时候用到了MVC三层架构，目的是为了实现高内聚低耦合，三层的关系如下：

![](http://ove4nglsb.bkt.clouddn.com/%E4%B8%89%E5%B1%82%E6%9E%B6%E6%9E%84.png)
View层控制页面的的展示
controller层实现页面的重定向，转发，参数传递。
service层内实现业务的业务逻辑。
DAO层实现对数据库的操作。
modal层也就是bean层，对象的实体层，里面主要有对抽象事物的属性和行为，用代码实现就是写的一些set和get方法以及私有的变量。
其中service层，DAO层，modal层都属于模型层。

现在controller层如果需要调用DAO层的方法，就需要通过创建Service层的实例，然后Service层创建DAO层的实例去控制数据库，这样子的缺点就是说一旦dao层里的路径一旦改变，service层，controller层也要跟着一起改，也就是说这三者之间的耦合度太高了，或者说三者之间的关联太紧密了，我们写代码追求的是高内聚低耦合，所以逐渐演变成了下面这种模式：使用工厂模式进行解耦合操作。

下面介绍进化版的创建实例的模式。
现在我有一个UserService类
```java
public class UserService{
    public void add(){
    }
}
```
按照以前的模式，如果需要调用UserService类中的add()方法，就需要创建UserService的对象然后通过类的对象来调用方法，现在我们提供一种工厂模式来解决，现在创建一个工厂类。
```java
public class Factory{  
    public static UserService getService(){
        return new UserService;    
    }
}
```
然后创建一个UserServlet类
```java
public class UserServlet{
//如果我们现在需要调用工厂类的方法来创建实例
    UserService s = Foctory.getService();
    s.add();
}
```
以上这种创建对象的方式就避免了直接new对象，而是通过工厂模式去实现对象的实例化，但是这种模式也有问题，就是说UserServlet和Factory也会出现关联，两者之间出现新的耦合度。于是出现了下面这种IOC的控制反转模式。

接下来就是再次进化版的创建实例的模式：IOC控制反转。
最开始有两个类，一个UserService类，一个UserServlet类
```java
puplic class UserService{
}
public class UserServlet{
}
```
第一步：创建XML配置文件，配置要创建的对象的类。
```xml
<bean id="userService" class="cn.liuenci.UserService"/>
```
第二步：创建工厂类,使用dom4j解析配置文件+反射
```java
public class UserFoctory{
    //返回UserService对象的方法
    public static UserService getService(){
        //使用dom4j解析XML文件
        //根据id值userService,得到id值对应class属性值
        String classValue = "class属性值";
        //使用反射创建类的对象
        Class c = Class.forName(classValue);
        //创建类对象
        UserService service = c.newInstance();
        return service;
    }
}
```
第三步：在UserServlet类中通过调用UserFactory类中的getService()方法即可创建对象。

为什么会使用这种方式去创建对象呢？是不是看起来挺简单的一个东西完全被Spring框架弄的复杂了呢？其实不是的，如果按照以前的方式使用new的方式创建对象的话，如果一个service类的对象路径一改，那么servlet也要改，但是这种IOC的模式就不要改那么多，因为我们提供的是XML方式，所以我们只需要改变XML文件中的class属性值即可。
以上就是IOC控制反转的底层实现原理，使用这种方式的原因也就是因为这种方式可以更好的完成了高内聚低耦合的操作，这就是技术的不断发展性，总有新的技术或者思想替代过去的陈旧的技术或者思想，我们程序员需要保持时刻学习的状态，才不会被互联网的浪潮淘汰掉。