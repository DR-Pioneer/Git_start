

microvideo内部GitLab地址在：[http://lab.microvideo.cn/](http://lab.microvideo.cn/)。注册好主动把账户发给mentor，mentor会把你加入到相应的项目中。

## 1.注册

![注册界面](https://pic4.zhimg.com/80/v2-57ad23ed4055c309e0178690b98b19d7.png)

注册之后，将你的用户名、邮箱等信息发给mentor，mentor会把你加入到相应的项目中。

## 2.创建项目

在初始界面右侧点击“New Project”按钮，进入创建项目界面。
![New Project](https://pic4.zhimg.com/80/v2-3c90e3970dd4fe45d035798b908dfab4.png)

新建项目主要分为三个情况：1.新建空项目；2.从现有项目导入；3.从模板导入。
![建项目](https://pic4.zhimg.com/80/v2-f8a8c23fb846a0809b21a2f534ee63a8.png)

根据自己的情况选择相应的选项，填写项目名称、项目描述、项目可见性等信息，点击“Create Project”按钮即可创建项目。

![Create Project](https://pic4.zhimg.com/80/v2-9fc3b5a603df9fb4629e57b4321a3768.png)

## 3.克隆项目到本地PC端

选择项目后，进入项目管理界面，找到项目的ssh地址，复制到剪贴板。也可以直接利用网址栏的地址，添加`.git`后缀，即可得到ssh地址。
![项目地址](https://pic4.zhimg.com/80/v2-13d2c13b9e82de852d2808272615f170.png)

在本地PC端，在需要放置项目的位置，右击打开`git bash here`，输入`git clone`命令，将项目克隆到本地。

```bash
git clone <项目ssh地址>
```

![克隆项目](https://pic4.zhimg.com/80/v2-084cd727618769a3a4d718d3cbe6d717.png)

## 4.初始化基本配置

### 4.1.配置用户名和邮箱

用户名，邮箱是git提交代码时的必要信息，用于显示提交者的信息。在克隆项目到本地后，需要配置用户名和邮箱。

```bash
# 配置用户名和邮箱
$ git config --global user.name "Your Name"
$ git config --global user.email "Your Email"
```

### 4.2.初始化项目

如果项目是克隆下来的，就不需要再次初始化项目（会自动配置好）。如果是本地新建的项目文件，想和gitlab上的项目关联，就需要初始化项目。

```bash
# 进入项目目录
$ cd <项目目录>

# 初始化项目，生成.git文件夹
$ git init

# 设置remote地址映射，origin是映射名称，可以自定义
$ git remote add origin <项目ssh地址>

# 查看remote地址映射
$ git remote -v
```

## 5.本地开发代码进行提交

### 5.1.开发代码

在本地文件夹中，进行开发代码，开发完成后，需要将代码提交到gitlab上。开发的过程中，如果有新的改进，尽可能的进行提交，这样可以保证代码的安全性。可以进行多次提交，也可以一次性提交。

> 注：在写到此处的时候，我就对文件进行了提交，这样可以保证代码的安全性。

![Image](https://pic4.zhimg.com/80/v2-10167bc44cb35e5203f9290ee2b80d0a.png)

可以使用`git status`命令查看当前文件的状态。`git status`命令用于显示当前代码库的状态，它会列出当前工作目录中已修改但还未提交的文件、已暂存但未提交的文件、还未跟踪的文件等信息。具体来说，git status命令可以帮助我们完成以下工作：

- 查看哪些文件被修改了，但还没有被暂存或提交。

- 查看哪些文件已经被暂存，但还没有被提交。

- 查看哪些文件是新添加的，但还没有被暂存或提交。

- 查看当前分支的名称，以及是否有未合并的改动。

```bash
# 查看当前文件状态
$ git status --porcelain
------------------------[输出结果]------------------------
M /path/to/modified/file.txt
?? /path/to/new/file.txt
A  /path/to/added/file.txt
```

其中，第一列表示文件的状态缩写，比如`M`表示文件已被修改但还未提交，`??`表示文件是新添加的，还未被Git跟踪，`A`表示文件已被添加到暂存区等等。第二列表示文件的路径。

如果你遇到中文文件名无法正常显示的情况，可以尝试通过设置Git的字符编码来解决，可以使用以下命令设置字符编码：

```bash
# core.quotepath用于指定Git是否对文件名进行转义，core.unicode用于指定Git是否启用Unicode支持。
$ git config --global core.quotepath false
$ git config --global core.unicode true
```

### 5.2.提交代码

在开发完成后，需要将代码提交到`gitlab`上。提交代码之前，需要将代码添加到暂存区，然后再提交。

```bash
# 添加文件到暂存区
$ git add <文件名> # 添加单个文件
$ git add . # 添加所有文件

# 添加文件注释
$ git commit -m "注释内容" # 注释内容格式：worknametime 修改的核心内容

# 拉去远程仓库代码，保持本地代码和远程代码一致，防止冲突
$ git pull origin master
# 其中，origin是远程仓库映射名称，master是分支名称

# 提交代码到远程仓库
$ git push origin master
```

> `pull`和`fetch`的区别，在拉取远程仓库代码时，如果本地代码和远程代码有冲突，`fetch`不会自动合并代码，而`pull`会自动合并代码。`pull = fetch + merge`。

在执行`fetch`命令之后，你可以通过以下操作来查看远程跟踪分支的更新情况：

- 使用`git branch -r`命令查看所有的远程分支以及它们所对应的远程跟踪分支。

- 使用`git log <remote>/<branch>`命令查看某个远程分支的更新历史记录。

- 使用`git diff <remote>/<branch>`命令查看某个远程分支与本地分支的差异。

### 5.3.利用VSCode进行代码提交

如果你是在VSCode中进行开发，也可以使用VSCode的Git插件进行代码提交。在VSCode中，按下`Ctrl+Shift+G`，打开Git插件，可以看到发现更改的文件。然后点击`+`，将代码添加到暂存区，然后点击`√`，进行代码提交。

![利用VSCode进行代码提交](https://pic4.zhimg.com/80/v2-014e7cfda2cda17cdad960456623fbef.png)

之后会跳出一个窗口，让你输入提交注释，输入注释后，点击`√`，完成代码提交。
![提交注释](https://pic4.zhimg.com/80/v2-b042832cb6dc11e265c6ffb538f5802b.png)

最后点击**同步更改按钮**，将代码同步到远程仓库。同时实现了`pull`和`push`的功能。

## 6.追溯代码

### 6.1.查看提交记录

在开发过程中，如果想查看提交记录，可以使用`git log`命令查看提交记录。

```bash
# 查看提交记录
$ git log --pretty=oneline
```

`git log --pretty=oneline`是一个常用的 Git 命令，它会显示提交历史记录，并以一行的形式展示每个提交的信息。

除了`oneline`外，`Git`还支持其他多种格式的提交历史记录展示方式，可以通过`--pretty`选项指定，比如：1.`%h`：缩短的提交对象的 SHA-1 校验和；2.`%an`：提交者的名字；3.`%ae`：提交者的邮件地址；4.`%s`：提交说明。

```bash
# 该命令将提交的 SHA-1 校验和、提交者的名字和提交说明按照自定义的格式输出。
$ git log --pretty=format:"%h %an %s"
```

### 6.2.追溯代码

如果你要追溯代码的修改历史，并还原某个特定版本的代码，可以使用 Git 的版本控制功能。

首先，你可以使用 git log 命令来查看提交历史记录。执行以下命令可以查看提交历史：

```bash
# 查看提交历史
$ git log --pretty=oneline
```

该命令会按照时间顺序显示提交历史，最新的提交会显示在最上面。

如果你想要还原某个特定版本的代码，可以使用`git checkout`命令，将代码回滚到该版本。执行以下命令可以回滚到某个特定版本：

```bash
# 回滚到某个特定版本
$ git checkout <commit-id> # commit-id是提交的id
# 或者使用sha
$ git checkout <commit-sha> # commit-sha是提交的sha
```

其中 `<commit-sha>`是你要回滚到的版本的 SHA-1 校验和。执行该命令后，你的代码库会还原到该版本，并且你可以查看、编辑该版本的代码。

> 需要注意的是，回滚到某个特定版本后，如果你对代码进行了修改并提交了新的版本，那么之前的版本就无法再次恢复。因此，在进行回滚操作时，一定要谨慎。

如果你想将本地的代码库也回滚到某个特定版本，可以使用`git reset`命令。

执行以下命令可以将本地的代码库回滚到某个特定版本：

```bash
# 回滚到某个特定版本
$ git reset --hard <commit-sha>
```

需要注意的是，`git reset`命令是一种比较危险的操作，因为它会彻底删除回滚版本之后的所有提交记录。如果你在执行`git reset`命令之后又进行了一些新的提交操作，那么这些提交记录将无法恢复。因此，在执行`git reset`命令时，一定要谨慎。

### 6.3.`git checkout`和`git reset`的区别

`git checkout`和`git reset`都是 Git 中常用的命令，它们在某些情况下可以实现相似的功能，但是它们的作用范围、作用对象以及对 Git 仓库中的不同部分产生的影响略有不同。

`git checkout` 命令用于切换分支或恢复文件。当你使用`git checkout` 切换分支时，Git 会将 HEAD 指针和工作目录切换到指定分支上，并将仓库中的所有文件替换为该分支上的文件。当你使用 `git checkout` 恢复文件时，Git 会将指定文件恢复到指定分支或提交中的版本。总之，`git checkout` 主要是用来操作工作区和 HEAD 指针的。

`git reset` 命令则用于撤销提交，可以将分支指针移动到指定提交上，并将暂存区和工作目录还原到该提交上的状态。`git reset` 的操作会影响到 Git 仓库中的提交历史，所以需要谨慎使用。

综上所述，`git checkout` 和 `git reset` 的区别主要在于它们的作用范围和作用对象。`git checkout` 主要是针对工作区和 HEAD 指针的操作，而 `git reset` 主要是针对 Git 仓库中的提交历史的操作。
