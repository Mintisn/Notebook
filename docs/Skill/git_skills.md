
# Git的快速使用
[参考文档戳这里](#参考文档)

## "创建新库"

创建并切换到latest_branch分支
git checkout --orphan latest_branch

添加所有文件
git add -A

提交更改
git commit -am "删除历史版本记录，初始化仓库"

删除分支
git branch -D master

将当前分支重命名
git branch -m master

强制更新存储库
git push -f origin master

## 速览
+ git init  //将该文件夹建立一个仓库  
+ git add * //将工作区所有保存文件加入到暂存区  
    + git add -u * //排除掉不被跟踪的文件
+ git commit -m "注释" //将暂存区文件提交到仓库引号里面可以适当加入一点注释
+ git reset --hard HEAD 回退到最新一次commit(当前版本),并且覆盖本地文件  
+ git push origin  
+ git pull  
+ git clone  
## 本地的常用操作

+ git init  //将该文件夹建立一个仓库
+ git add * //将工作区所有保存文件加入到暂存区
+ git add *.txt //将后缀txt的文件加入到暂存区
+ git commit -m "第一次提交" //将暂存区文件提交到仓库引号里面可以适当加入一点注释

这些都只是提交版本回顾以一下流程  
首先是必须初始化 git init  
之后不必初始化  
每次提交时,需要先add,才能commit  
如果commit的文件没有变化.git会给出提示  
需要注意的是  
如果你add的文件本身就没保存,那么自然文件时没有变化的,所以记得先在  
vscode中保存文件  

以上全是提交,且不涉及分支(建议学会回滚之后再学分支,感觉平时自己写代码不怎么需要分支,一个主分支就够自己用)
下面介绍一个回滚以前版本的操作

比如
+ git reset HEAD^ 回退到上个版本
+ git reset --hard HEAD 回退,,并且覆盖本地文件
注意到,没有hard参数时时不会覆盖本地文件的
表现为你明明回滚了,看到的文件却没有变化(本身你希望直接文件全部改变)

再注意到,如果只是想回滚到上次提交commit,只需要
+ git reset --hard HEAD
就好了

这些都是基本操作,这些操作本身还有很多其他参数.各自又不同功能

例如 reset 操作有 --hard --soft 等等
但只要学会以上操作,其他更复杂的参数也会很容易理解

另外,如何链接github账号上的远程仓库啥的,也可以去学一学

## 参考文档
> [菜鸟Git教程](https://www.runoob.com/git/git-tutorial.html)