#### 为什么有权限
在一个系统中，如果只有一个用户，那有没有权限都无所谓，但是如果在一个系统上有多个用户的时候，为了避免其他用户对重要文件的查看修改等操作，所以就出现了权限的概念。
#### 如何查看权限
查看文件的权限只需要输入以下命令即可查看。
```
ls -l
```
![Linux文件权限](http://ove4nglsb.bkt.clouddn.com/03-01-02.png)
图片来源:https://morvanzhou.github.io/tutorials/others/linux-basic/3-01-file-permissions/ 侵删。

类似于 drwxrwxr-x 这种格式的就是文件的权限。细节展示在上面的图中，下面解释一下这个字符串的四个部分。
* Type:文件的类型，(- 为文件，d 为文件夹，其他的还有 l,n,有需求再搜)
* User:在 Type 后面紧跟着的三个空就是说是用 User 的身份能对这个做什么处理(r 能读；w 能写；x 能执行；- 不能完成某个操作)，User 一般指的是当前使用电脑的人。
* Group:一个 Group 里面可能有一个或者多个 User,这些权限的样式和 User 一样。
* Others:除了 User 和 Group 以外人的权限。
#### 如何修改权限
先看一个例子，如何给 User 添加执行权限
```
chmod u+r file.py
```
归纳一下得到以下公式
```
chmod [谁][怎么修改][修改哪个文件]
```
u+r 就是说给 User 加上 read 权限，给 file.py 这个文件进行修改。
[谁]
* u:修改 User
* g:修改 Group
* o:修改 Others
* a:修改 all
[怎么修改]
* +,-,= : 加上，剪掉，等于某些权限
* r,w,x : 或者多个权限一起，比如 rw.
