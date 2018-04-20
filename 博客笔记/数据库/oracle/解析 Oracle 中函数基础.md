#### 什么是函数
函数就是一组 SQL 语句或者 PL/SQL 语句块的集合，同时可以返回执行结果。

#### 函数语法
```sql
CREATE [OR REPLACE] FUNCTION function_name
 (arg1 [ { IN | OUT | IN OUT }] type1 [DEFAULT value1],
 [arg2 [ { IN | OUT | IN OUT }] type2 [DEFAULT value1]],
 ......
 [argn [ { IN | OUT | IN OUT }] typen [DEFAULT valuen]])
 [ AUTHID DEFINER | CURRENT_USER ]
RETURN return_type
 IS | AS
    <类型.变量的声明部分>
BEGIN
    执行部分
    RETURN expression
EXCEPTION
    异常处理部分
END function_name; 　
```

#### 如何创建函数
下面是一个求阶乘的函数
```sql
create or replace function jiecheng(n int) return int is
num_ int := 1;
i int;
begin
  for i in 1 .. n loop
    num_:=num_*i;
  end loop;
  return num_;
end;
```
然后执行函数
```sql
select jiecheng(5) from dual;
```

#### 函数如何调用
函数声明时所定义的参数叫做形参，然后调用函数时传进去的值成为实参。调用函数一般有以下三种方法向函数传递参数：
1. 位置表示法，就是严格按照形参的声明顺序来进行调用，例如函数：
```sql
create or replace function function_name(a int,b varchar2(10),c number(4,2)) ..
```
那么调用就必须按照 abc 的顺序来进行调用。
```sql
function_name(1,'test',3.2)
```
2. 名称表示法
这种表示法对次序没有要求，但是对参数之间的对应有要求，具体格式如下：
```sql
function_name(a => 1,b => 'test',c => 3.2)
```
3. 组合传递法
这种方式就是同时调用位置表示法和名称表示法为函数传递参数。这种表示法的要求就是，只要其中有一个参数使用名称表示法，那么后面的参数都需要使用名称表示法。具体格式如下：
```SQL
function_name(1,b=>'test',c=>3.2)
```

#### 关于参数的 IN,OUT,IN OUT 以及 函数参数默认值
IN,OUT,IN OUT 都是形参的模式，如果省略，那么则都是 IN 输入模式，这种模式只能输入，也就是只能读不能写，而 OUT 则相反，只能输出，不能输入，也就是只能写，不能读，IN OUT 则是既能读又能写。

函数参数的默认值在创建函数的时候就已经确立，在函数调用时没有提供实参的情况下会使用默认值，当提供实参时会使用实际值，只能为输入参数提供默认值，而不能为 OUT 和 IN OUT 提供默认值。
