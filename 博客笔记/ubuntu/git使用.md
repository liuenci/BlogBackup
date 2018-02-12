#### git使用
参考文章：http://www.xgllseo.com/?p=5428
感谢大神。

下面是我挣扎了三天各种重装Ubuntu系统之后开始使用git的一点小经验。
1. 测试git是否安装
```
git --version
```
记住一定是--,不是一个-。
2. 获取ssh密钥
```
ssh-keygen -C "你的github邮箱" -f ~/.ssh/github
```
执行的过程中会提示你需要设置密码，不要管它，一路回车。
这时候会在你的～/目录下面生成一个.ssh/目录，但是Ubuntu默认是不显示这个目录的。查看.ssh目录下的github.pub获取公钥认证，就是一串乱码。
接下来获取这串乱码。
```
cd .ssh
sudo gedit github.pub
```
这个时候会打开这个文件，只需要复制里面的代码到github里面的SSH and GPG keys 里面填写一下就好了。
3. 创建本地项目文件
这个文件就是专门负责项目的上传和更新，进入这个文件夹，然后在终端输入以下代码
```
git clone "你的github仓库地址"
```
4. 提交文件夹到github上
```
git add . // 更新整个目录
git config user.name "liuenci" //第一次需要配置
git config user.email "154910381@qq.com" //第一次需要配置
git commit -m "更新版本简要说明"
git push -u origin master
```
这样子就能够上传我们的项目了。
