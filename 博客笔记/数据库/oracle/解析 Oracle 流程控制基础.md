这篇文章简单的介绍一下一些 Oracle 中的流程控制怎么使用。

## 条件语句
### if 语句
```sql
DECLARE
  salary emp.sal%TYPE;
  empno_ emp.empno%TYPE;
BEGIN
  empno_ := &请输入员工编号;
  SELECT sal INTO salary FROM emp WHERE empno = empno_;
  IF salary > 2000 THEN
    dbms_output.put_line('土豪');
  ELSIF salary BETWEEN 1000 AND 2000 THEN
    dbms_output.put_line('小康');
  ELSE
    dbms_output.put_line('屌丝');
  END IF;
END;
```
### case 表达式
```sql
SELECT CASE grade
  WHEN 1 THEN '一级'
  WHEN 2 THEN '二级'
  ELSE '更高级' END
FROM salgrade;
```

## 循环语句
### 简单循环
```sql
DECLARE
  i INT := 0;
BEGIN
  LOOP
    i := i + 1;
    dbms_output.put_line(i);
    EXIT WHEN i = 100;
  END LOOP;
END;
```
### while 循环
```sql
DECLARE
  i INT := 0;
BEGIN
  WHILE i < 100 LOOP
    dbms_output.put_line(i);
    i := i + 1;
  END LOOP;
END;
```
### 数字式循环 for in n..m loop
```sql
DECLARE
  i INT := 0;
BEGIN
  FOR i IN 0..100 LOOP
    dbms_output.put_line(i);
  END LOOP;
END;
```
### 顺序语句
```sql
DECLARE
  i INT;
BEGIN
  i := &input;
  IF i = 2 THEN
     GOTO label1;  
  END IF;
  <<label1>> -- label1之后什么也不做需要运行 null 语句
  NULL;
END;
```
