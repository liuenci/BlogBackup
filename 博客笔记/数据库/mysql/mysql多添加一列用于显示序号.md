因为项目的主键是从1001开始的，但是页面上要求从1开始，可以通过使用给mysql设置变量来完成。
具体代码如下
```mysql
set @rownum = 0;
select *,@rownum := @rownum + 1 from user;
```
