---
date: 2018-01-21 15:33
status: public
title: Spring如何注入对象属性
---

由于比较简单，所以直接贴代码和步骤，最后总结一下关键点。
> 创建一个UserDao类
```java
package cn.liuenci.ioc;

public class UserDao {

	public void add() {
		System.out.println("DAO");
	}
}
```
> 创建一个UserService类
```java
package cn.liuenci.ioc;

public class UserService {

	private UserDao userDao;
	
	public void setUserDao(UserDao userDao) {
		this.userDao = userDao;
	}

	public void add() {
		System.out.println("SERVICE");
		
		userDao.add();
	}
}
```
> 配置XML文件
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	
	<!-- 注入对象属性 -->
	<bean id="userDao" class="cn.liuenci.ioc.UserDao"></bean>
	<bean id="userService" class="cn.liuenci.ioc.UserService">
		<property name="userDao" ref="userDao"></property>
	</bean>
	
</beans>
```
总结:
1. 写UserService类时需要写set方法，get方法可以不用，因为我们只需要注入对象，而且一般set注入属性会比较多，使用构造方法注入也可以，但一般使用set注入。
2. 配置XML时注意要先注入UserDao的对象，然后注入需要调用UserDao的方法的对象，另外需要注意的就是属性中对象的值的标签不是用 value 了，而使用 ref (引用) 来注入对象属性。