以前一直用的 oracle11g，每次安装都没有 sql developer,今天 google 看到原来 11g 好像没有内置 sql developer,并且删除了 scott 用户，又解决了我一个使用 oracle 的困惑。

下面讲讲如何创建 scott 用户并且授予权限。

参考链接如下：http://blog.csdn.net/btt2013/article/details/52554514

##### 使用数据库管理员身份登陆账户
在这一步之前你先要保证自己的数据库服务启动，这里我就不说了，然后打开 sql plus 之后登陆。输入口令直接回车即可。
```
sys  as sysdba;
```
##### 创建用户并且设置密码
```
create user scott identified by 123456;
```
##### 授予权限
由于我在安装 oracle 的时候把创建为容器数据库给取消了，所以授予权限有一点点不同。
```
grant connect,resource,unlimited tablespace to scott;
```
如果创建容器数据库可以使用下面这行语句
```
grant connect,resource.unlimited tablespace to scott container=all;
```
##### 设置用户使用的表空间
```
alter user scott default tablespace users;
alter user scott temporary tablespace temp;
```
##### 使用 scott 用户登录
```
connect scott/123456;
```
##### 显示当前用户
```
show user;
```
