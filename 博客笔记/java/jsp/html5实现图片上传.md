### 前言
话说现在成熟的框架写一个文件上传挺简单的，但是因为直接学习框架中的文件上传会造成一种只会调用别人写好的代码来实现功能，但是自己并不会其中的原理的一种尴尬的情况，所以还是自己把图片上传用原生的js+servlet实现一下。

### 首先是前端页面
前端页面因为是只需要实现一个功能，就只写一个form表单即可。
```html
<form id="form">
	<input type="file" name="file_upload" />
	<button type="button" onclick="upload()">上传</button>
</form>
```
### 然后写一个js
js中的每一步的原理都已经注释在代码中了，这里就不再赘述了。其中要注意的是需要使用FormData包装数据。使用FormData可以使发送表单数据更方便，因为FormData对象是可以使用一系列的键值对来模拟一个完整的表单，然后使用XMLHttpRequest发送这个"表单"。
```javascript
function upload() {
	// 获取表单对象
	var form = document.querySelector("#form");
	// 创建请求对象
	var ajax = new XMLHttpRequest;
	// 设置请求方式和路径
	ajax.open("post", "upload");
	// 使用FormData包装数据
	var fd = new FormData(form);
	// 发送请求
	ajax.send(fd);
	// 处理请求
	ajax.onreadystatechange = function() {
		if (ajax.readyState == 4 && ajax.status == 200) {
			// 接受返回的数据
			var data = ajax.responseText;
		}
	}
}
```
### 最后写后端的Servlet文件（因为我是Java开发）
因为get方式提交的文件的大小有限，加上安全性不好所以使用post提交方式，所以我们只需要重写doPost方法即可。
```java
package com.liuenci.ajax;

import java.io.IOException;
import java.util.UUID;

import javax.servlet.ServletException;
import javax.servlet.annotation.MultipartConfig;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.Part;

@WebServlet("/upload")
@MultipartConfig
public class Upload extends ServletImpl {
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		forward("upload");
	}
	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		// 接收文件
		Part p = req.getPart("file_upload");
		// 获取提交的文件名
		String submitName = p.getSubmittedFileName();
		// 重新生成文件名
		String newName = UUID.randomUUID().toString();
		String kzm = submitName.substring(submitName.lastIndexOf("."));
		// 组合名字
		String newFile = newName+kzm;
		// 组合保存路径
		String pt = req.getServletContext().getRealPath("/upload");
		String path = pt+"\\"+newFile;
		// 保存
		p.write(path);
	}
}
```
### 特别提醒
1. WebContent文件夹下面需要建一个upload文件夹，并且需要放置一张图片，因为不放图片空文件夹不会上传到tomcat中。
2. Tomcat的server Location需要设置server path成tomcat的安装目录，Deploy path设置成Tomcat中的webapps文件夹。
