前面写过一个用原生的js写的文件上传，今天就把原生的ajax也写一下吧，毕竟这个东西还是很常用的。
我先把代码贴上来。
### html代码
```html
<button type="button" onclick="get()">get请求</button>
<button type="button" onclick="post()">post请求</button>
```
### js代码
```javascript
function get(){
	// 创建请求对象
	var ajax = new XMLHttpRequest;
	// 设置请求方式和路径
	ajax.open("get","ajax?name=zhangsan");
	// 发送请求
	ajax.send();
	// 处理请求
	ajax.onreadystatechange = function(){
		if(ajax.readyState ==4 && ajax.status == 200){
			// 更新数据
			var data = ajax.responseText;
			alert(data);
		}
	}
}
function post(){
	// 创建请求对象
	var ajax = new XMLHttpRequest;
	// 设置请求方式和路径
	ajax.open("post","ajax");
	// post请求提交参数，必须要设置头部类型
	ajax.setRequestHeader("Content-type","application/x-www-form-urlencoded");
	// 发送请求
	ajax.send("name=zhangsan");
	// 处理请求
	ajax.onreadystatechange = function(){
		if(ajax.readyState == 4 && ajax.status == 200){
			// 更新数据
			var data = ajax.responseText;
			alert(data);
		}
	}
}
```
### 后端servlet代码
```java
package com.liuenci.ajax;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/ajax")
public class TestAjax extends ServletImpl {
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		String name = req.getParameter("name");
		System.out.println(name);
		resp.getWriter().print(name);
	}
	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		String name = req.getParameter("name");
		System.out.println(name);
		resp.getWriter().print(name);
	}
}
```
### 总结
ajax:一种请求数据的方式，不需要刷新整个页面。

ajax的核心技术是 XMLHttpRequest 对象。

ajax请求过程：创建XMLHttpRequest对象、连接服务器、发送请求、接收响应数据。
1. 创建对象

IE7以上版本直接用
```javascript
var ajax = new XMLHttpRequest();
```
创建即可

2. 连接和发送

open()函数有三个参数：请求方式、请求地址、是否异步请求（同步比较少，我就只写两个参数了）。

get请求方式是通过url链接后面带参数提交到服务器的，post是将数据作为send()的参数提交到服务器的。

post请求中，在发送数据之前，必须设置表单提交的内容类型。

3. 接收
接收到响应后，响应的数据会自动填充XHR对象，相关属性如下：

responseText:返回字符串类型，现在开发基本上是返回一个json数据。

responseXML：如果响应的内容类型是"text/xml"或者"application/xml",这个属性中将保存着相应的xml数据，是xml的document类型。

status:响应的HTTP状态码。

statusText:HTTP状态的说明。

4. ajax对象的readyState属性表示请求/响应过程的当前活动阶段，这个属性的值如下

0-未初始化，尚未调用open()方法

1-启动，调用了open()方法，没有调用send()方法

2-发送，已经调用send()方法，未接收到响应。

3-接收，已经接收到部分响应数据。

4-完成，已经接收到全部响应数据。

5. ajax.status是状态码，状态码以2开头的都是成功，304表示从缓存中获取。

6. ajax请求是不能跨域的。

参考链接：http://caibaojian.com/ajax-jsonp.html，侵删。
