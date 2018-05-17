## 错误截图
![](http://ove4nglsb.bkt.clouddn.com/sql%20%E5%91%BD%E4%BB%A4%E6%9C%AA%E6%AD%A3%E7%A1%AE%E7%BB%93%E6%9D%9F.png)

## 错误原因
仔细看一下日志发现我的 sql 是这么写的。

```xml
UPDATE dept set dname = ? and loc = ?  where deptno = ?
```
and ？？？？
更新语句中如果有多个更新的地方是使用 (,) 逗号隔开。

## 错误原因二
当我们的 sql 语句后面有 (;) 的时候也会报这个错误。
