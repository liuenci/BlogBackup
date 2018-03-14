因为自己老是忘记 git 上传的步骤，每次上传文件都要重新谷歌找答案，所以
干脆写下来记录一下。

1. 在github上创建仓库，创建仓库的时候勾选初始化readme文件

2. 如果是从来没有上传过github的代码，则执行以下代码。

3. 先初始化git的本地仓库。
```
git init;
```
4. 再将readme文件从云端拉下来，这样云端仓库中的readme文件就到自己本地来了
```
git pull "github仓库地址"
```
5. 将文件提交到缓存区,2.x版本的git两个命令都是一样都能将被删除的文件提交到缓存区
```
git add .
// 或者 git add -A
```
6. 提交一个版本到本地仓库
```
git commit -m "message"
```
6. 添加远程仓库分支
```
git remote add origin "github地址"
```
7. 将本地master分支的代码推送到远程仓库origin的master分支
```
git push -u origin master.
// 我试了下下面这个命令也是正确的可以上传的
git push origin master
```

###### 总结
git 的学习是一门大学问，技术是永远学不完的，只能一点一点慢慢学，遇到问题解决完再进行总结才能得到最大的收益，这样才能避免下次再出这样的错误。
