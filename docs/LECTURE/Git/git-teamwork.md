# Git 合作开发实例：eesast 开发

说明：团队仓库名为`eesast`，个人仓库名为`yxj`

## 将远程仓库下载、链接到本地

### 克隆原仓库到本地

```shell
git clone <eesast.url> --origin eesast <project_new_name>
```

`--origin <远程仓库名>`用来给默认的名字origin重命名

`--origin`:`-o`

`<project_new_name>`指本地新出现的文件夹的名称

### fork仓库使得自己有push的权限

在`GitHub`上操作，得到自己fork后的仓库链接`<yxj.url>`

### 进入clone后的仓库


```shell
cd <project>
```

### 添加自己的远程仓库


```shell
git remote add yxj <yxj.url>
```

`add`后紧跟的是远程仓库的名字，可以自定义

### 查看关联的远程仓库

```shell
git remote --verbose
git remote --verbose show eesast
git remote --verbose show yxj
```

`--verbose`:`-v`

## 开始开发自己的功能

注：一般团队仓库只有一个master分支

### 先拉取最新内容

```shell
git fetch eesast
```

### 将最新的内容merge到自己的master分支

```shell
git checkout master
(master) git merge eesast/master
```

这里应该不会遇到冲突，因为本地不会在master分支进行开发，除非你修改文件的时候忘记切换到新的分支

### checkout到新的分支

```shell
git checkout -b modify
```

### 开始自己修改代码

#### 拉取最新的代码

如果你在`checkout -b`之后一直把改代码这件事情扔在一边儿，那么你在开始修改之前最好再拉取一下最新的信息进行合并：

```shell
git fetch eesast
(modify) git merge eesast/master
```

#### 修改

比如增加文件、删除文件，增加代码、删除代码等

#### 提交

```shell
(modify) git add .
(modify) git commit -m"modify sth"
```

#### 拉取最新代码查看是否有冲突

在上一次commit之后，再次修改代码之前，你需要拉取最新的代码；这时可能会遇到冲突，因为你在本地修改的时候别人可能已经在远端仓库提交了PR并且被管理者merge到新的代码中。遇到冲突需要自己解决

```shell
git fetch eesast
(modify) git merge eesast/master
```

在解决冲突后再次commit；如果无冲突则没有必要commit

```shell
(modify) git add .
(modify) git commit -m"solve conflicts"
```

#### 再次修改

重复上述“修改”，“提交”，“拉取最新代码”的过程

## push到远端和提PR

### push到自己的仓库

```shell
git push yxj modify:modify
```

这里的语法是：`git push <远程主机> <本地分支>:<远程分支>`

含义：将某一本地分支推到远程主机的远程分支；如果远程仓库没有这一分支，则创建

也可以写作：

```shell
(modify) git push yxj modify
```

这里的语法是：`git push <远程主机> <远程分支>`

含义：将本地的当前分支推到远程主机的远程分支；如果远程仓库没有这一分支，则创建

### 提PR

登陆`GitHub`，在你的仓库可以拿着刚刚推到远程的modify分支向团队仓库提一个PR

### 等待开发者merge

如果PR被拒绝，你可以继续更改代码、commit、push、提PR直到merge；也可以直接弃坑lol

## 开发者merge之后删除modify分支

### 删除远程分支

#### 方法一

在团队仓库的PR界面，如果成功merge，那么你可以看到一个`delete branch`的按钮，可以直接点击按钮删除自己fork的仓库中的modify分支

#### 方法二

```shell
git push yxj --delete modify
```

#### 方法三

```shell
git push yxj :modify
```
这里的语法是：`git push <远程主机> :<远程分支>`（注意和push到远端仓库做区分）

### 删除本地分支

```shell
(master) git branch -d modify
```

确认删除可以使用：

```shell
(master) git branch -D modify
```

### 可能遇到的问题

使用`git fetch --all`将所有远端仓库（eesast和yxj）的最新“状况”拉取到本地

这时使用命令`git branch -a`查看所有分支，发现远端yxj的modify分支并没有删除

这说明不能通过git fetch命令获取到分支删除的更新

使用`git remote -v show yxj`查看分支状况，发现modify分支是陈旧的（stale）

使用`git remote prune yxj`删掉本地陈旧的远端分支（就是

远端已经删除掉了但是本地还没删除掉的分支）

或者拉取信息的时候使用：

```shell
git fetch -p --all
```

## References

[CSDN | Git远程分支的删除与同步](https://blog.csdn.net/dta0502/article/details/90214417)

[Git Documentation](https://git-scm.com/docs)
