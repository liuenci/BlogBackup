---
date: 2017-11-29 15:42
status: public
title: 'oracle check约束总结'
---

1. 创建表的时候创建约束
* 定义为列的约束
```oracle
create table KCB2
(
课程号 varchar2(10) not null,
课程名 varchar2(10) not null,
开课学期 number(1) null,
学时 number(2) null,
学分 number(1) check(学分>=0 and 学分<=10) not null --定义为列的约束
)
```
un* 定义为表的约束
```oracle
create table books
(
book_id number(10),
book_name varchar(50) not null,
book_desc varchar2(50) default 'new book',
max_lvl number(3,2) not null,
trade_price number(4,1) not null,
constraint ch_cost check(max_lvl<=250)
)
```