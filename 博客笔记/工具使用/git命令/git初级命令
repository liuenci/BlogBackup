这篇文章用来记录自己学习git时所遇到的一些命令。
1. 设置全局的用户名和邮箱
```git
git config --global user.name "cier"
git config --global user.email "154910381@qq.com"
```
2. 查看设置的用户名和邮箱
```git
git config user.name
git config user.email
```
3. 清屏
```git
clear
```
4. git初始化
```git
git init
```
5. 显示隐藏文件
```git
ls -a
```
6. 生成文件
```git
touch 1.py
```
7. 查看文件状态，看是否有文件没有添加到我们的git版本库中
```git
git status
```
8. 简单的拉取代码操作
```git
git pull "https://github.com/liuenci/Git-Test.git"
```
这个可以在新建一个仓库并且初始化有readme.md的文件时使用
9. 查看日志
```git
git log
```
10. 查看此次add和上次commit的两个版本之间的不同
```git
git diff
```
还有一种查看方式是
```
git diff --cached
```
具体是啥我也没弄懂，以后要是找到答案再补上
11. add所有的改变的文件
```
git add .
```
12. 将日志一行一行打印
```
git log --oneline
```
13. 补充上一次提交的内容，并且不改变commit的message,但是commit ID改变了
```
git commit --amend --no-edit
```
14. add 之后想要继续更改其中的内容，可以选择回退
```
git reset 1.py
```
15. reset回到HEAD指针所在的版本
```
git reset --hard HEAD
```
16. 回退到当前版本的第 n 个版本,把 n 替换成你想要回退的版本即可
```
git reset --hard HEAD~n
```
17. 回到指定的commit ID 的版本
```
git reset --hard 7757af1
```
18. 查看所有的日志，包括未来的。
```
git reflog
```
19. 单个文件的版本回退
```
git checkout
git checkout 7757af1 -- 1.py
```
20. 使用图形的方式打印日志，一般用于多分支的情况
```
git log --oneline --graph
```
21. 查看所有的分支
```
git branch
```
22. 创建分支
```
git branch dev
```
23. 切换分支
```
git checkout master
```
24. 删除分支
```
## 没有合并的分支
git branch -D dev
```
26. 建立分支的同时将head指针移动到新创建的分支
```
git checkout -b dev
```
27. 在add的同时commit，这种方式只适合于当前版本库中已经有的文件，新创建的文件无法被是被
```
git commit -am "新创建的文件无法识别"
```
28. 在当前分支上合并其它分支的内容
```
git merge --no-ff "合并的message" dev
```
29. 简单的合并分支
```
git merge dev
```
30. 另外一种合并分支的方式
```
git rebase dev
```
31. 将未完成的工作暂存在缓存区。
```
git stash
```
32. 将暂存区中的内容拿出来
```
git stash pop
```
33. 忽略windows和unix换行符
```
git config --global core.autocrlf false
```
