#### Ubuntu基础命令
###### cd 切换位置
移动到 Document
```
cd Documents
```
移动到上一级目录
```
cd ..
```
返回到 Home 目录
```
cd ~
```
返回到你刚刚所在的目录
```
cd -
```
去往电脑的任何一个位置,使用的是绝对位置
```
cd /home/cier
```
##### ls 浏览文件
显示当前目录下所有文件（不包括隐藏文件）
```
ls
```
显示当前目录下文件的详细信息
```
ls -l
```
显示所有文件，包括隐藏文件
```
ls -a
```
更人性化的显示文件
```
ls -lh
```
显示 ls 所有的功能
```
ls --help
```
##### touch 创建文件
创建一个文件
```
touch file1
```
创建多个文件
```
touch file1 file2 file3 file4 file5
```
##### cp 复制文件或者文件夹
将老文件复制到新文件
```
cp file1 file1copy
```
如果file1copy已经存在，上面的语句会直接覆盖原来的file1copy,为了避免覆盖，需要在cp后面加一个选项。回复任意大小写的'y'或者'yes'就确认复制，直接回车或者输入其他字母会取消复制，
```
cp -i file1 file1copy
```
复制进文件夹
```
cp file1 folder1/
```
复制文件夹，需要加上 -R (recursive)
```
cp -R folder1/ folder2/
```
复制文件名称部分相同的文件
```
cp file* folder2/
```
复制单独的几个文件到另外一个文件夹
```
cp file1 file1copy file2 folder1/
```
#####　mv 移动文件
移动一个文件到另外一个文件夹
```
mv file6 folder1/
```
移动文件到原来的地点，但是以不同的名字，就是重命名
```
mv file1 file1rename
```
找到更多的 mv 的操作
```
mv --help
```
##### mkdir 创建文件夹
在当前目录添加一个文件夹
```
mkdir folder3
```
在文件夹中建一个文件
```
mkdir folder3/file1
```
##### rmdir 移除文件夹
rmdir 就是 remove directory 的意思，但是这个命令只能删除文件夹内没有文件的文件夹。也就是说只能移除空文件夹。
```
rmdir folder3
```
##### rm 移除文件
移除单个文件
```
rm file1
```
有提示的移除文件
-i 每个要移除的文件都进行提示
-I 超过三个要移除的文件才进行提示
```
rm -i file1 file2 file3
rm -I file*
```
删除非空文件夹,加上 -r 或者 -R
```
rm -r folder1
```
##### nano 编辑脚本
打开一个python脚本进行编辑,编辑完之后 ctrl+x 保存，再通过 python 指令运行
```
nano file.py
python file.py
```
##### cat 查看脚本内容,或者将脚本中的内容写进另外一个脚本中
查看 python 脚本内容
```
cat file.py
```
将文件的内容写进另外一个文件，另外一个文件不存在时会自动创建
```
cat file.py > file2.py
```
将多个文件写进另外一个文件，另外一个文件不存在时会自动创建,内容顺序为 file1 file2 file3
```
cat file1.py file2.py > file3.py
```
将一个文件写入到另外一个文件的末尾
```
cat file1.py >> file2.py
```
