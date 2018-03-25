---
date: 2017-11-21 16:04
status: public
title: oracle错误总结
---

1. 在scott用户方案下创建视图出现 ORA-01031，用户权限不足，说明scott用户没有创建视图的权限，可以登录sysdba账户，执行以下语句即可。
```oracle
grant select any table , create view to scott;
```
2. ORA-01861: 文字与格式字符串不匹配,执行一下语句即可
```oracle
alter session set nls_date_format = "YYYY-MM-DD";
```