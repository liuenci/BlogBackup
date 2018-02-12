---
date: 2017-12-26 14:07
status: public
title: oracle设置自增序列
---

> oracle和mysql的自增区别

mysql自增使用的是auto increment，但是oracle中需要使用序列配合触发器来实现自增。
> 步骤1:创建表

```oracle
create table classroom
(
c_id NUMBER(4) not null primary key,
c_address VARCHAR2(10) not null,
c_count NUMBER(2) not null
);
```
> 步骤2：创建序列
```oracle
create sequence class_id_increment
INCREMENT by 1
start with 1001
maxvalue 1999
nocycle
```
> 步骤3：创建触发器
```oracle
create TRIGGER class_id_trigger
before insert on classroom for each row when (new.c_id is null)
BEGIN
SELECT class_id_increment.nextval into :new.c_id from dual;
end;
```
> 步骤4：插入语句测试
```oracle
insert into classroom VALUES(1001,'101',50);
INSERT into classroom(c_address,c_count) VALUES('102',60);
INSERT into classroom(c_address,c_count) VALUES('103',70);
```
以上的插入语句中后两条在不插入主键的情况下，使用序列和触发器完成了主键编号自增。