JSP(1)
1. 什么叫JSP:
	1. 全称：java server pages
	2. JSP是一种动态网页编程语言，将java作为脚本，为网页提供服务器数据。
	3. 在传统的HTML代码中加入java程序片段和jsp标记。所以jsp也可以理解为HTML+Java。

2. JSP优点：
	1. write once,run anywhere.一次编写，到处运行。
	2. 跨平台：JSP是基于java开发的，所以具有跨平台特性，可以在windows，linux等系统上运行。
	3. 组件重用：使用javaBean编写业务组件，在jsp页面，或者整个项目中可以进行重复使用。
	4. 多样化和功能强大的开发工具支持。记事本，eclipse，editplus.
	5. 服务器：Tomcat,JBoss,WebLogic等。
	6. asp.net:简单易学，但是安全性和跨平台性差。
	7. php:简单，高效，成本低开发周期短，特别适合中小型企业。常用的开发环境：LAMP:linux+Apache+mysql+PHP。
3. JSP劣势：
	1. 增加产品的复杂性(部署难度)：使用JSP为了获得它的跨平台和扩展性。就必须要将Java的各种产品的组件有效的组合起来，才能发挥它的优势(jar,jdk,ejb,javabean...)。
	2. 对硬件的要求高(性价比低)：java高速运行时将.class常驻在内存中来实现，另外还需要空间保存java和.class文件，所以系统需要的内存和用户数就比较低。
	3. 调试难度大：JSP页面被访问的时候，是将JSP转换为java文件，再编译为.class文件。先转换，在编译，再解释运行。所以如果程序出错，错误信息实际上指向的是java文件，而不是jsp页面。
	
	
4. Tomcat的目录结构
	1. bin:存放执行命令和执行文件。tomcat的启动(startup.bat),关闭文件(shutdown.bat)。如果启动失败，有可能是JDK配错了。
	2. lib：存放Tomcat运行时需要的jar库和公共的jar库文件。
	3. conf：存放tomcat配置文件
	4. temp:存放临时文件
	5. logs:存放服务器日志文件
	6. webapps:web项目默认的部署目录，所有的项目都存放在这里。
	7. work:存放JSP页面转换的java文件
