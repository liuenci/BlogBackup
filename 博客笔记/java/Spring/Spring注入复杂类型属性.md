---
date: 2018-01-21 16:47
status: public
title: Spring注入复杂类型属性
---

前面几篇文章讲了一下字符串属性注入，对象属性注入，p名称空间注入，这篇文章讲一下如何注入复杂类型的属性例如：
1. 数组
2. List
3. Map
4. Properties
步骤如下：
> 新建一个Person类
```java
package cn.liuenci.property;

import java.util.List;
import java.util.Map;
import java.util.Properties;

public class Person {

	private String[] array;
	private List<String> list;
	private Map<String,String> map;
	private Properties properties;
	public void setArray(String[] array) {
		this.array = array;
	}

	public void setList(List<String> list) {
		this.list = list;
	}

	public void setMap(Map<String, String> map) {
		this.map = map;
	}

	public void setProperties(Properties properties) {
		this.properties = properties;
	}

	
	public void test() {
		System.out.println("array:"+array);
		System.out.println("list:"+list);
		System.out.println("map:"+map);
		System.out.println("properties:"+properties);
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
	<!-- 复杂属性注入 -->
	<bean id="person" class="cn.liuenci.property.Person">
		<!-- 数组注入 -->
		<property name="array">
			<list>
				<value>a</value>
				<value>b</value>
				<value>c</value>
			</list>
		</property>
		<!-- list集合注入 -->
		<property name="list">
			<list>
				<value>e</value>
				<value>f</value>
				<value>g</value>
			</list>
		</property>
		<!-- map集合注入 -->
		<property name="map">
			<map>
				<entry key="a" value="aa"></entry>
				<entry key="b" value="bb"></entry>
				<entry key="c" value="cc"></entry>
			</map>
		</property>
		<!-- properties注入 -->
		<property name="properties">
			<props>
				<prop key="driverclass">com.mysql.jdbc.driver</prop>
				<prop key="name">root</prop>
				<prop key="password">123456</prop>
			</props>
		</property>
	</bean>
</beans>
```
这里的话掌握一下使用的格式应该就可以了，数组和List的注入方式一样，Map和Properties的注入方式类似，记住他们之间的相似点和不同点即可。
> 新建一个测试TestIOC类
```java
package cn.liuenci.property;

import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class TestIOC {
	@Test
	public void testUser() {
		// 1. 加载spring配置文件，根据配置文件创建对象
		ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
		// 2. 得到创建配置的对象
		Person person = (Person)context.getBean("person");
		person.test();
	}
}
```
运行结果如下:
![](http://ove4nglsb.bkt.clouddn.com/%E5%A4%8D%E6%9D%82%E5%B1%9E%E6%80%A7%E6%B3%A8%E5%85%A5.png)
