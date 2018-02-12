---
date: 2018-01-17 11:06
status: public
title: 'Spring Bean的三种实例化方式'
---

第一种：使用无参构造方法进行实例化
> 创建User类
```java
package cn.liuenci.ioc;

public class User {
	public void add() {
		System.out.println("add");
	}
}
```
> 新建XML文件
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	<bean id="user" class="cn.liuenci.ioc.User"></bean>
</beans>
```
> 创建TestIOC类
```java
package cn.liuenci.ioc;

import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class TestIOC {
	@Test
	public void testUser() {
		// 1. 加载spring配置文件，根据配置文件创建对象
		ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
		// 2. 得到创建配置的对象
		User user = (User) context.getBean("user");
		System.out.println(user);
		user.add();
	}
}
```
这种方式创建对象是最方便的，关键在于XML文件声明一个id属性和class属性即可。

第二种：使用静态工厂模式进行实例化
> 创建User类
```java
package cn.liuenci.ioc;

public class User {
	public void add() {
		System.out.println("add");
	}
}
```
> 创建UserFactory类
```java
package cn.liuenci.ioc;

public class UserFactory {
	public static User getUser() {
		return new User();
	}
}

```
> 创建XML文件
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	<!-- 静态工厂创建对象 -->
	<bean id="user" class="cn.liuenci.ioc.UserFactory" factory-method="getUser"></bean>
</beans>
```
> 创建TestIOC文件
```java
package cn.liuenci.ioc;

import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class TestIOC {
	@Test
	public void testUser() {
		// 1. 加载spring配置文件，根据配置文件创建对象
		ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
		// 2. 得到创建配置的对象
		User user = (User) context.getBean("user");
		System.out.println(user);
		user.add();
	}
}
```
这是第二种bean的实例化方法，关键点在于1、创建工厂类；2、配置xml文件中的factory-method属性值为工厂类中的获得对象的方法。

第三种：通过实例工厂进行对象实例化
> 创建User类
```java
package cn.liuenci.ioc;

public class User {
	public void add() {
		System.out.println("add");
	}
}
```
> 创建实例工厂类
```java
package cn.liuenci.ioc;

public class UserFactory {
	public User getUser() {
		return new User();
	}
}
```
> 创建xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	<bean id="userFactory" class="cn.liuenci.ioc.UserFactory"></bean>
	<bean id="user" factory-method="getUser" factory-bean="userFactory"></bean>
</beans>
```
> 创建TestIOC文件
```java
package cn.liuenci.ioc;

import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class TestIOC {
	@Test
	public void testUser() {
		// 1. 加载spring配置文件，根据配置文件创建对象
		ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
		// 2. 得到创建配置的对象
		User user = (User) context.getBean("user");
		System.out.println(user);
		user.add();
	}
}
```
这是第三种bean的实例化方式，关键在于1、创建一个不是静态方法的工厂类，这种类的特点就是需要实例化才能调用方法。2、配置xml文件中第一步需要实例化实例工厂类，第二步配置factory-method属性和factory-bean方法。