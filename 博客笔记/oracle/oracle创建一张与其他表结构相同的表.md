---
date: 2017-11-28 16:30
status: public
title: oracle创建一张与其他表结构相同的表
---

> 这段时间学习Oracle的时候要建立一张日志表，创建一个触发器，如果在学生表中删除了数据，需要在xsb_his表中进行备份。

1. 只建立结构，不导入数据
```oracle
create table xsb_his as select * from xsb where 1=0;
```
2. 既建立结构，又要导入所有数据
```oracle
create table xsb_his as select * from xsb where 1=1;
```