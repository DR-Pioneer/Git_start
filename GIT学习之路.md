# GIT学习之路

### 1、git init

初始化本地仓库

### 2、git remote add + 仓库名字 + 链接地址

### 3、git remote -v

fetch 将代码从远程仓库取出

push 将代码从本地推送到远程仓库

git remote remove + 仓库名字 不想连接这个远程仓库了

### 4、 将文件添加至暂存区

git add  + 文件名，...文件名  将多个文件加到暂存区

git add + 文件夹名/*.html 将xx文件夹下的所有的html文件添加到暂存区。

git add . 提交新文件（new）和 被修改的文件，不包括删除的文件

**git add -A 提交所有变化**

### 5、描述更改的用户和日志消息

git commit -m "修改注释"  你现在可以简单的理解为给你刚才add的东西加一个备注，你上传到远程仓库之后，修改的文件后边会显示这个备注

### 6、将文件推到远程仓库

git push -u 仓库名称 分支

仓库名称：刚才我添加连接的时候，给仓库起名叫origin

分支：你现在只有主分支，所以分支直接写master。以后合作项目的时候，成员之间建了不同的分支，你就可以往你自己的分支上推。

 `–u`参数才会把本地的master分支和远程的master分支关联起来，就是告诉远程仓库的master分支，我的本地仓库和是对着你的哦，不是对着别的分支的哦。
只有第一次推的时候需要加上`-u`，以后的推送只输入：git push 名称 分支

git push origin master -f  强制推送 可能会覆盖掉远程的数据

### 7、查看命令提交记录

- git log

- git log --pretty=oneline

抢救commit的注释

- git commit --amend -m "修改的内容"


### 8、文件下拉

push会报错的情况下，代表远程仓库和本地仓库有数据被修改了

上边push报错，我自己知道数据差在哪里，所以使用了强制推送。但是在团队合作中，push报错，那铁定是你队友修改了远程仓库，如果你再强制上传，那你就是毁了你队友的代码。所以如何保证在你修改之前，自己的文件跟远程仓库一致呢。

---- git pull 仓库名称

pull = fetch + merge

**git fetch 并没更改本地仓库的代码，只是拉取了远程数据，git merge才执行合并数据。**



### 总结

回想一下你刚才是怎么push到远程的

- git add添加到上传缓存区
- git commit给缓存区的内容添加备注，此时本地的commit修改啦，但是远程的commit和文件都没修改。
- git push 修改远程文件和commit信息

而你下拉文件过程

- git fetch 将数据拉下来，但是没修改本地的commit和文件
- git merge 改变本地数据



### 9、文件克隆

仓库是你自己的，你就使用SSH连接，不是你自己的，你没权限你就切换到HTTPS，再复制地址。它克隆下来是一个文件夹，你想把文件夹放哪里就在哪打开gitbash

git clone + 复制的github地址

git remote -v吗？用它看一下你下下来的本地仓库连接上那个远程仓库没。



### 10、git分支

```git
git branch: 查看当前仓库的分支情况
git branch + 分支名称：创建新的分支
切换分支：
    git checkout + 分支名称：切换到新分支下
    git switch + 分支名称：切换到新分支下(高版本下)
恢复文件到上一个版本：
	git checkout + <commit-id> / <commit-sha>
合并分支：（切换到主分支下后，执行）
	git merge dev(分支)
中止合并：	
	git merge --abort
分支删除：
	git branch -d + 分支名 （只删除已完成合并的分支）
	git branch -D + 分支名 （强制删除分支）

合并->冲突
	git diff: 查看冲突内容
	
HEAD指针：
	指向不同分支最新的提交纪录，不同的分支会有一个共同的提交祖先
```

### 11、git几种模式的使用

```git
一、git对自己仓库的使用，权限是不受控制的,随意拉取，释放
二、git团队协作时，按权限分为两种模式：
   1、社区仓库禁止其他人直接修改，需fork到自己的仓库中，修改完成后，向社区仓库提交merge申请
   2、master，other branch分支可以作为团队协作的形式，但这是一种默契约定，团队内的成员依然能够切换到主分支直接merge其他分支。
```

### 12、git 回退命令

```
一、git reset [--soft --mixed(默认) --hard] <commit id>
soft: 回退到某一版本，保留工作区和暂存区的内容
hard: 回退到某一版本，丢弃工作区和暂存区的内容
mixed: 回退到某一版本，只保留工作区，丢弃暂存区的内容

git ls-files 显示暂存区中全部文件的路径
```

### 13、git push失败

```
当我们在github版本库中发现一个问题后，你在github上对它进行了在线的修改；或者你直接在github上的某个库中添加readme文件或者其他什么文件，但是没有对本地库进行同步。这个时候当你再次有commit想要从本地库提交到远程的github库中时就会出现push失败的问题。
问题：problem->failed to push some....
解决方案：-> git pull --rebase + "仓库名字" + master(分支名字)
原理：-> 将远程库的更新合并到本地库中，rebase取消本地库刚才的commit,并将其接到更新后的版本库中

```









