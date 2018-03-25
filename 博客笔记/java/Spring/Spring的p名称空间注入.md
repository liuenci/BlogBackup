---
date: 2018-01-21 16:17
status: public
title: Spring的p名称空间注入
---

因为不是很常用，所以就只贴下代码和步骤明白如何使用即可。
> 创建Person类
```java
package cn.liuenci.property;


public class Person {

	private String name;
	
	public void setName(String name) {
		this.name = name;
	}
	
	public void test() {
		System.out.println("person:"+name);
	}
}
```
> 配置xml文件
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:p="http://www.springframework.org/schema/p"
	xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">	
	<!-- p名称空间注入 -->
	<bean id="person" class="cn.liuenci.property.Person" p:name="lucy"></bean>
</beans>
```
这一步需要着重讲一下一些重要的点：
1. 我这里新建了一条语句就是
```xml
xmlns:p="http://www.springframework.org/schema/p"
```
它其实就是下面这条语句的变体
```xml
xmlns="http://www.springframework.org/schema/beans"
```
这一步其实就是新建了一个叫做p的名称空间。
2. 使用p名称空间注入
```xml
<bean id="person" class="cn.liuenci.property.Person" p:name="lucy"></bean>
```
就是在标签中加了一句
```xml
p:name="lucy"
```
实现的p名称空间的注入方式
> 测试类

略，这里写一个单元测试然后测试一下test方法即可。