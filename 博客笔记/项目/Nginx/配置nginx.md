1. 安装
解压即可。
2. 导入配置文件
在nginx.conf中加入
```
include vhost/*.conf;
```
3. 建文件夹vhost
4. 建两个配置文件
分别为image.imooc.com,tomcat.imooc.com.加入配置代码。
image.imooc.com中监听端口为80，自动建立索引，访问的域名为image.imooc.com,输入这个域名访问的本机的文件夹地址是E:\ftpfile\img;
配置为
```
server {
    listen 80;
    autoindex on;
    server_name image.imooc.com;
    access_log c:/access.log combined;
    index index.html index.htm index.jsp index.php;
    #error_page 404 /404.html;
    if ($query_string ~* ".*[\;'\<\>].*") {
        return 404;
    }
    location ~ /(mmall_fe|mmall_admin_fe)/dist/view/* {
		deny all;
	}
	location / {
		root E:\ftpfile\img;
		add_header Access-Control-Allow-Origin *;
	}
}
```
tomcat.imooc.com的监听端口是80，自动建立索引，要访问的域名为tomcat.imooc.com,代理的路径是tomcat的本机ip，端口是8080；
```
server {
    listen 80;
    autoindex on;
    server_name tomcat.imooc.com;
    access_log c:/access.log combined;
    index index.html index.htm index.jsp index.php;
    #error_page 404 /404.html;
    if ($query_string ~* ".*[\;'\<\>].*") {
        return 404;
    }
    location / {
        proxy_pass http://127.0.0.1:8080;
        add_header Access-Control-Allow-Origin *;
    }
}
```
5. 配置hosts文件
hosts文件在
```
C:\Windows\System32\drivers\etc
```
在hosts文件中加入
```
127.0.0.1 image.imooc.com

127.0.0.1 tomcat.imooc.com
```

### 总结
这样nginx就差不多配置完了，然后启动tomcat之后在浏览器中输入
```
tomcat.imooc.com
image.imooc.com
```
如果显示有东西即可。
