Java 中的对象创建有很多种，比如我所知道的以下几种：
1. 通过 new 关键字分配内存去创建对象
2. 通过反射机制创建对象
3. 通过 clone() 方法复制对象
4. 通过 Spring 中 @Autowired 注解自动装配
5. 通过 xml 对 bean 的配置，再在 Java 类中通过创建应用上下文，以及 getBean(Class class) 方法创建对象。

## 谈谈 clone() 方法
先看一下普通的通过 new 关键字创建对象。
```java
Student student = new Student();
Student student1 = student;
System.out.println(student);
System.out.println(student1);
```
输出结果：
```java
com.spring.pojo.Student@64729b1e
com.spring.pojo.Student@64729b1e
```
从输出结果可以看出来 student 和 student1 的地址是相同的，所以他们指向的是同一个 Student 对象。这种就是简单的引用的赋值。

再来看看 clone() 方法。

首先 Student 学生类需要实现 Cloneable 接口，并且重写 clone() 方法，如果调用 Student 类的 clone() 方法在其他包类，还需将 clone() 方法开放为 public 权限。
```java
@Override
public Object clone() throws CloneNotSupportedException {
    return super.clone();
}
```
然后 clone Student 对象。
```java
Student student = new Student();
Student student1 = (Student) student.clone();
System.out.println(student);
System.out.println(student1);
```
输出结果：
```java
com.spring.pojo.Student@64729b1e
com.spring.pojo.Student@10bbd20a
```
从两者的地址来看，两个 student 指向的不同的对象，也就是说 clone() 方法是开辟了另外的空间并且创建了另外的 Student 对象。
