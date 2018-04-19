oracle 中存在伪列这个说法，它就像一个表的列一样，但是它并不存储在表中，伪列可以从数据库中查出，但是无法对伪列进行更新，删除和插入。常用的伪列就有 ROWNUM 和 ROWID.
#### ROWNUM 伪列
ROWNUM 伪列是 oracle 首先从数据库中查询到一个结果集，然后再在结果集上加上一个伪列，伪列的作用就是在结果集中添加一个从 1 开始的序列号。例如以下 sql.
```sql
select rownum,deptno from dept;
```
结果如下：

![](http://ove4nglsb.bkt.clouddn.com/rownum.png)

通过结果可以看到如果我们需要获取某个数据集下的前 10 条数据的话就可以通过判断 rownum 的大小即可。例如：
```sql
select rownum,deptno from dept where rownum <= 10;
```

由于 rownum 是先有结果集，再添加伪列，并且伪列都是从 1 开始的，所以以下语句会查不到任何结果。
```sql
select rownum,deptno from dept where rownum >=2 and rownum <= 4;
```
如果想要得到想要的结果，可以使用子查询的方法。例如：
```sql

select rownum,deptno from (select rownum num,deptno from dept) where num >=2 and num <= 4;
```
结果如下：

![](http://ove4nglsb.bkt.clouddn.com/TIM%E6%88%AA%E5%9B%BE20180419093212.png)

#### ROWID 伪列
ROWNUM 是物理上不存在的，但是 ROWID 是物理上存在的，它的作用是用来唯一标识一条记录物理位置的一个 ID,类似于 Java 中的一个对象的哈希码，都是为了标识对应对象的物理位置。

利用 ROWID 的唯一特性，可以用 ROWID 来进行去重。
例如创建一个表：
```sql
CREATE TABLE dept_bak AS SELECT * FROM dept;  
INSERT INTO dept_bak SELECT * FROM dept;
```
查询表中的数据:
```sql
select rowid,dept_bak.* from dept_bak;
```
结果如下：

![](http://ove4nglsb.bkt.clouddn.com/rowid.png)
最后利用 rowid 进行去重。
```sql
DELETE FROM dept_bak WHERE ROWID NOT IN( SELECT MIN(ROWID) FROM dept_bak GROUP BY DEPTNO);
```
这样就完成了利用 rowid 的唯一特性去重了。
