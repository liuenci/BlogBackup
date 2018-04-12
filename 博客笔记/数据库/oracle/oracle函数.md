### 单行函数

#### 日期函数
##### 获取系统日期
```
sysdate
```

java 中日期格式化：yyyy-MM-dd HH:mm:ss

mysql 中日期格式化：%Y-%m-%d %H:%i:%s

oracle 中日期格式化：yyyy-mm-dd hh24:mi:ss

##### 格式化日期
```
to_char(sysdate,'yyyy-mm-dd hh24:mi:ss')
```
##### 将字符串转换为日期
```
to_date('2000-01-22','yyyy-mm-dd hh24:mi:ss')
```
##### 添加月份
```
select add_months(sysdate,2) from dual
```
##### 返回指定月的最后一天
```
select last_day(sysdate) from dual
```
##### 计算两个日期之间相差多少月
```
select months_between(sysdate,add_months(sysdate,4)) from dual
```
##### 返回下一个日期
```
select next_day(sysdate,2) from dual
```
星期日 = 1  星期一 = 2  星期二 = 3  星期三 = 4  星期四 = 5  星期五 = 6  星期六 = 7
##### 返回日期/时间的单独部分，比如年月日时分秒等等
```
-- sysdate中只能获取年月日
select extract(year from sysdate) from dual;
select extract(month from sysdate) from dual;
select extract(day from sysdate) from dual;
-- 时分秒需要在
```
