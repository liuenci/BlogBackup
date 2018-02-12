> 这一次咱们谈谈JavaWeb中涉及到的路径问题。

---
路径分为两种：
* 绝对路径
* 相对路径

绝对路径是指具体到某个项目工程下面具体的某个文件夹下的某个文件，好像有点绕，后续详细展开。

相对路径则比较难懂，因为经常弄混，所以我打算用具体的实例来谈谈jsp中关于相对路径的问题。

> 第一种：jsp页面在WEB-INF下面的某个具体的文件夹下面。跳转方向：从servlet跳转到jsp页面。

首先假设我们的目录结构是这样的。


![](http://ove4nglsb.bkt.clouddn.com/%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84.png)


如果你想要访问的jstlTest.jsp页面在WEB-INF下面的jstl下面，那么你是无法直接通过http://localhost:8080/elandjstl/WEB-INF/jstl/jstlTest.jsp这个链接访问到的。它会报404错误，也就是找不到这个页面。

解决方法：通过转发或者重定向访问这个页面。我们可以看到我在cn.liuenci这个包下面有个EL.java文件，这个文件具体是一个servlet文件，我们通过doGet(request,response)或者doPost(request,response)两个方法中使用重定向或者转发可以访问到这个页面。具体代码如下，两句代码择一即可。
```java
//转发
request.getRequestDispatcher("WEB-INF/jstl/jstlTest.jsp?num=9").forward(request, response);
//重定向
response.sendRedirect("WEB-INF/jstl/jstlTest.jsp?num=9");
```
跳转的路径需要加上WEB-INF/文件夹1/文件夹2/.../文件夹n/文件.jsp

> 第二种：jsp页面就在WebContent根目录下面。跳转方向：从servlet跳转到jsp页面。

我在WebContent的根目录下面新建了一个test.jsp文件。项目结构是这样的:

![](http://ove4nglsb.bkt.clouddn.com/%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%842.png)

这个文件是可以直接通过地址访问到的。地址：http://localhost:8080/elandjstl/test.jsp
如果我们要从servlet跳转到这个jsp页面，也可以使用重定向或者转发。具体代码如下：

```java
//转发
request.getRequestDispatcher("test.jsp").forward(request, response);
//重定向
response.sendRedirect("test.jsp");
```

> 第三种：在WEB-INF文件夹下面的jsp页面要访问src里面的servlet文件做doGet或者doPost处理。跳转方向：jsp跳转到servlet

这里我们不能直接在WEB-INF文件夹下面那个jsp页面使用重定向或者转发，因为直接运行该jsp页面会报404错误，我们先要在WebContent文件夹根目录下面创建一个jsp页面，在该页面中使用转发或者重定向跳转到WEB-INF下面那个jsp页面，然后在该jsp页面使用表单提交到servlet里面进行处理。