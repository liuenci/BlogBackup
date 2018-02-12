---
date: 2017-11-20 16:02
status: public
title: oracle总结
---

1. oracle 12c默认的日期格式是"DD-MM月-YY",修改默认的日期格式代码:
```oracle
alter session set nls_date_format = "YYYY-MM-DD"
```
2. 创建表的时候可以声明具体的单位,char(2char)表示两个字符，如果不在括号中写char，char(2)表示是两个字节。
```oracle
create table XSB
(
学号 CHAR(6) NOT NULL PRIMARY KEY,
姓名 CHAR(8) NOT NULL,
性别 CHAR(2char) DEFAULT '男' NOT NULL,
出生时间 date NOT NULL,
专业 char(12) null,
总学分 number(2) null,
备注 varchar2(200) null
);
```
3. 列的约束主要有五种:not null,unique,primary key ,reference table,check.分别是非空，唯一，主键，外键，检查约束。
4. 如何创建一个表的备份表,表后面可以加where条件
```oracle
create table xs_jsj as select * from xsb where 专业='计算机'
```
5. 添加表的字段
```oracle
alter table xs_jsj add (奖学金等级 number(1),等级说明 varchar2(40) default '奖金1000元')
```
6. 修改默认值
```oracle
alter table xs_jsj modify (等级说明 default '奖金800元')
```
7. 删除列
```oracle
alter table xs_jsj drop column 奖学金等级
```
8. 创建表创建主键，注意主键的名字不能是单引号包裹，单引号会报错。
```oracle
alter table xs_jsj add (constraint "pk_jsj" primary key(学号))
```
9. 删除表
```oracle
drop table xs_jsj
```
10. insert into语句可以将一个表中的数据插入进另外一张表中
```oracle
insert into xsb1 select 学号 姓名 专业 from xsb where 姓名 = '王林'
```
11. merge关键字的使用,下面这段代码的意思是如果学号匹配，就把a表中的数据更新成XSB中的数据,如果不匹配，那就插入这条记录。
```oracle
merge into A 
using xsb on (a.xh=xsb.学号)
when matched 
  then update set a.xm = xsb.姓名,a.xb=xsb.性别,a.cssj=xsb.出生时间,a.zy=xsb.专业,a.zxf=xsb.总学分,a.bz=xsb.备注
when not matched
  then insert values(xsb.学号,xsb.姓名,xsb.性别,xsb.出生时间,xsb.专业,xsb.总学分,xsb.备注);
```
12. 空值的比较
```oracle
select * from cp where 备注 is not null
```
13. all关键字的使用
```oracle
select * from xsb where 出生时间 < all (select 出生时间 from xsb where 专业='计算机')
```
14. EXISTS子查询，EXISTS谓词用于测试子查询的结果是否为空表，若子查询的结果集不为空，则exists返回true，否则返回false。
```oracle
select 姓名 from xsb where exists (select * from cjb where 学号 = xsb.学号 and 课程号 = '206')
```
15. 在写存储过程代码遇到一个如何执行存储过程的问题，算是一个小坑，我先贴上代码。
```oracle
--查询某人的总学分
create or replace procedure update_info (vxh in char) as
xf number;
begin
  select zxf into xf from xsb where xh = vxh and rownum = 1;
  if xf>50 then
    update xsb set bz = '三好学生' where xh = vxh;
  else
    update xsb set bz = '三差学生' where xh = vxh;
  end if;
end;
--执行存储过程
exec update_info(vxh=>'101101')
```
执行存储过程的时候我最开始用的代码是
```oracle
exec update_info(vxh>='101101');
```
仔细看书上我发现存储过程的赋值是这样的是使用的 '=>'
```oracle
exec update_info(vxh=>'101101');
```