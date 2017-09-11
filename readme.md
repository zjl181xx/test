# GIT

### 1.使用流程

+ 使用命令  `Git init`   初始化版本管理（创建当前项目的Git管理仓库）（**切换项目目录**）
  + 创建一个当前项目的 版本管理文件 .git
  + 针对于项目进行初始化，一个项目一个管理仓库


+ 直接做项目开发

### 2.文件状态

+ git管理是基于文件的状态进行管理，
+ 文件新增状态
+ 文件删除状态
+ 文件修改状态
+ 文件的管理是一个手动的管理（需要使用者提供管理节点的）



### 3.常用命令

+ `git status`  文件状态查询

```
ITANY-IMAC-137:git-demo appleuser$ git status
On branch master      ----- 当前项目分支 为 master 主分支 

Initial commit        ----- 初始化提交

Untracked files:      ----- 没有被git管理的文件
  (use "git add <file>..." to include in what will be committed)

	01.html

nothing added to commit but untracked files present (use "git add" to track)
```



```
ITANY-IMAC-137:git-demo appleuser$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   01.html    ----  文件被修改

no changes added to commit (use "git add" and/or "git commit -a")
```



+ `git add [filename]`   提交文件被git管理  （只是告知给git 需要被管理的文件有哪些）
+ `git add --all`     （配合.gitignore）提交所有文件的修改

```
ITANY-IMAC-137:git-demo appleuser$ git add 01.html    ---- 新文件的增减
ITANY-IMAC-137:git-demo appleuser$ git status         ---- 文件状态的查询
On branch master   

Initial commit

Changes to be committed:     ---- git 中存在文件被修改
  (use "git rm --cached <file>..." to unstage)

	new file:   01.html    ---- 新增的文件  (没有被真正的管理)
```

+ `git commit -m '描述信息'`   添加管理节点

  ```
  ITANY-IMAC-137:git-demo appleuser$ git commit -m '01.html 文件新增第一次文件提交'

  [master (root-commit) 2b85da9] 01.html 文件新增第一次文件提交   ---- 提交的分支 版本号 描述信息

   Committer: AppleUser <appleuser@ITANY-IMAC-137.local>    ---- 默认用户名和邮箱
   
  Your name and email address were configured automatically based
  on your username and hostname. Please check that they are accurate.
  You can suppress this message by setting them explicitly. Run the
  following command and follow the instructions in your editor to edit
  your configuration file:

      git config --global --edit

  After doing this, you may fix the identity used for this commit with:

      git commit --amend --reset-author

   1 file changed, 10 insertions(+)    ----  几个文件被修改   几行代码被修改
   create mode 100644 01.html
  ```

  + windows 下 第一次安装的 git  是不能直接使用改命令
  + `git config --global user.name '姓名'`    配置提交者姓名
  + `git config --global user.eamil '邮箱'`  配置提交者的邮箱
  + `git config --global user.name`    查询提交者姓名
  + `git config --global user.eamil`  查询提交者的邮箱



+ `git diff`  比较当前文件的代码和 最后一次提交的代码之间的 变换（区别）

```
ITANY-IMAC-137:git-demo appleuser$ git diff
diff --git a/01.html b/01.html
index e4d2b91..daef694 100644
--- a/01.html
+++ b/01.html
@@ -5,8 +5,8 @@
        <title>Document</title>
 </head>
 <body>
-       <h1>学习GIT</h1>
-       <h2>1</h2>
-       <h2>2</h2>
+       <h3>1</h3>
+       <h3>2</h3>
+       <h3>3</h3>
 </body>
 </html>
\ No newline at end of file
```



+ `git reset --hard '版本号前六位'`    做指定版本的回滚

```
ITANY-IMAC-137:git-demo appleuser$ git reset --hard 9f58c3
HEAD is now at 9f58c39 01.html 文件修改
```



+ `git log`  查看当前项目中 所有的 git 的版本(**当前项目的版本之前的版本**)
  + `--all-macth`   

```
ITANY-IMAC-137:git-demo appleuser$ git log
commit 9f58c392e4ccf3acf1c191d42988aad6da770f9c    ---- 版本号   (hash 算法  HASH值)
Author: itany <itany@itany.com>        ----   提交者
Date:   Mon Sep 11 09:51:04 2017 +0800     ---- 提交时间

    01.html 文件修改      ----  提交时的信息日志

commit b6f8e36d532a2b0c8c1decc76599d64e390ad3e0
Author: itany <itany@itany.com>
Date:   Mon Sep 11 09:50:17 2017 +0800

    01.html 文件修改

commit 2b85da9b92377d1cbf69916636c835b9d8cf4133
Author: AppleUser <appleuser@ITANY-IMAC-137.local>
Date:   Mon Sep 11 09:43:22 2017 +0800

    01.html 文件新增第一次文件提交
```



+ `git reflog`     查看在当前项目中执行的所有操作



+ `--help`     对主命令的子命令进行查看   帮助文档
  + `q`   退出帮助文档或显示列表



### 4.远程仓库的使用

+ `github`     开源项目公开的git仓库
+ `git remote add 名称 地址`    第一一个远程 仓库的地址和名称
  + `git remote -v`   查看远程仓库的配置信息 
+ `git push -u 远程地址 分支名称`     （master）     将本地代码提交到服务器
+ `git pull 远程地址`    获取当前项目版本的远端代码
+ `git clone 远端地址`   从远端获取 项目的完成信息



+ 代码冲突 的解决方式
  + 1、放弃本地版本    重新 reset 到上次同步的版本，进行代码的操作
  + 2、版本的合并
    + `git stash`    当前代码备份  （在内存中备份的   代码放在 内存堆栈空间中）
    + `git stash pop`    返回合并备份代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<h1>学习GIT</h1>
	<h2>1</h2>
	<h2>2</h2>
	<h2>3</h2>
	<h3>4</h3>
<<<<<<< HEAD
	<p>本地新增</p>      <!-- 本地添加的代码  -->
=======
	<div>在线修改</div>      <!-- 远端的代码和版本号 -->
>>>>>>> 43866e3a14ce71c760943e3cbc53526a91fe4b85
</body>
</html>
```



### 5.文件忽略配置项

+ .gitignore    定义是不需要被提交的文件 （不需要被git 管理的文件）
+ 每一行都表示一个忽略文件



### 6. git 分支维护

+ `git branch`   查看当前项目的所有分支
+ `git branch -a`   查看当前项目中的所有分支
+ `git checkout 分支名`  分支的检出和维护
+ `git branch 分支名`     创建一个新的分支







































































