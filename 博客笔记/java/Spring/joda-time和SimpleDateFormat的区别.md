> 参考链接：http://jjhpeopl.iteye.com/blog/2321528
#### joda-date和SimpleDateFormat的相同点
两者都是对日期的格式化操作。

#### joda-date和SimpleDateFormat的不同点

joda-date 是线程安全的，SimpleDateFormat是线程不安全的，如果多个线程同时操作一个 SimpleDateFormat 实例，就会对 Calendar 的赋值进行覆盖，进而产生问题。


joda-date 依赖于第三方的 maven 配置，具体配置如下：
```maven
<!--?xml version="1.0" encoding="UTF-8" standalone="no"?--> <dependency>
  <groupId>joda-time</groupId>
  <artifactId>joda-time</artifactId>
  <version>2.9.4</version>
</dependency>
```
SimpleDateFormat不依赖于第三方包，直接 jdk 支持。

##### 如何解决 SimpleDateFormat 在高并发情况下的时间处理问题
1. 在每次需要使用的时候，进行SimpleDateFormat实例的创建，这种方式会导致创建一些对象实例，占用一些内存，不建议这样使用。

2. 使用同步的方式，在调用方法的时候加上synchronized，这样可以让线程调用方法时，进行加锁，也就是会造成线程间的互斥，对性能影响比较大。

3. 使用ThreadLocal进行保存，相当于一个线程只会有一个实例，进而减少了实例数量，也防止了线程间的互斥，推荐使用这种方式。
