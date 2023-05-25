# Git 实例

## git init/add/status/diff/commit/status/add/commit/log/diff

### 初始化仓库

```
$ cd ~/Desktop
$ mkdir notes
$ cd notes
$ git init
Initialized empty Git repository in /Users/yangxijie/Desktop/notes/.git/
```

### 添加一个文件

```
$ touch markdown_learn.md
$ vim markdown_learn.md
$ cat markdown_learn.md
# Markdown Note
# Grammar
`#`: title

[](): add link

![](): add image
```

### 查看状态

```
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	markdown_learn.md

nothing added to commit but untracked files present (use "git add" to track)
```

### 添加文件到暂存区

```
$ git add markdown_learn.md
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   markdown_learn.md
```

### 再添加一篇文件

```
$ touch git_learn.md
$ vim git_learn.md
$ cat git_learn.md
# Git Note
# About Git
Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

# Git Commands
`git add <file>`
`git commit -m "<msg>"`
```

### 查看状态

```
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   markdown_learn.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	git_learn.md
```

### 修改文件

```
$ vim markdown_learn.md
# Markdown Note
# Grammar
`#`: title

[](): add link

![](): add image

**bold_text**

*italic_text*
```

### 再次查看状态

```
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   markdown_learn.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   markdown_learn.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	git_learn.md
```

### 添加gitignore

我们希望一次添加这两个文件，在这之前先创建`.gitignore`：

```
$ touch .gitignore
$ echo ".DS_Store" >> .gitignore

$ git add .
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   .gitignore
	new file:   git_learn.md
	new file:   markdown_learn.md
```

### 提交

```
$ git commit -m "add two notes"
[main (root-commit) bdf79c8] add two notes
 3 files changed, 19 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 git_learn.md
 create mode 100644 markdown_learn.md
```

### 查看状态

```
$ git status
On branch main
nothing to commit, working tree clean
```

### 添加和提交

```
$ vim git_learn.md
$ cat git_learn.md
# Git Note
# About Git
Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

# Git Commands
`git add <file>`
`git commit -m "<msg>"`
`git status`

$ git add .
$ git commit -m "add new git commands"
[main c874462] add new git commands
 1 file changed, 1 insertion(+)
```

### 查看log

```
$ git log
commit c874462dba874eb098a4445f8ff6a15b2e381fc7 (HEAD -> main)
Author: yxj <564197835@qq.com>
Date:   Thu May 20 20:42:43 2021 +0800

    add new git commands

commit bdf79c8b45ebdd1e7644d0a19b47b8c4cba84f9a
Author: yxj <564197835@qq.com>
Date:   Thu May 20 20:40:03 2021 +0800

    add two notes
```

### 比较差异

比较两次commit的差异（其中前面有加号的是第二次提交添加的，剩下的信息并不那么重要）：

```
$ git diff bdf79c c87446
diff --git a/git_learn.md b/git_learn.md
index 575b88e..1b60d22 100644
--- a/git_learn.md
+++ b/git_learn.md
@@ -5,3 +5,4 @@ Git is a free and open source distributed version control system designed to han
 # Git Commands
 `git add <file>`
 `git commit -m "<msg>"`
+`git status`
```

## git restore

TODO

## git brancn/switch

### 新建仓库

```
$ cd ~/Desktop
$ mkdir teamwork
$ cd teamwork
$ git init
```

### 添加文件在main分支至少有一次commit

```
$ touch README.md
$ echo  'This is our teamwork!'  >> README.md
$ cat README.md
This is our teamwork!
$ git add README.md
$ git commit -m "add README"
[main (root-commit) 605051f] add README
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

### 在sayHello分支上写代码

```
$ git branch -c sayHello
$ git switch sayHello
Switched to branch 'sayHello'
$ touch sayHello.swift
$ vim sayHello.swift
$ cat sayHello.swift
func sayHello(name: String) {
    print("Hello, \(name).")
}
$ git add sayHello.swift
$ git commit -m "add func sayHello"
[sayHello e30ff7a] add func sayHello
 1 file changed, 3 insertions(+)
 create mode 100644 sayHello.swift
```

### 回到main分支进行合并

```
$ git switch main
Switched to branch 'main'
$ git merge sayHello
Updating 605051f..e30ff7a
Fast-forward
 sayHello.swift | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 sayHello.swift
$ git log
 Untracked files:
commit e30ff7a9797f9577b056c91cdbc46b37bff71168 (HEAD -> main, sayHello)
Author: yxj <564197835@qq.com>
Date:   Fri May 21 18:37:09 2021 +0800

    add func sayHello

commit 605051f10e676b477d5f101dca5828cf34165ab6
Author: yxj <564197835@qq.com>
Date:   Fri May 21 18:30:57 2021 +0800

    add README
```

### 在goodMorning分支上写代码

同上述`在sayHello分支上写代码`的内容，之后也是回到`main分支`进行合并

## 向GitHub上的开源项目提交代码

TODO
