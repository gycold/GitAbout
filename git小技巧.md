+ 文档红色：未add，仅仅存在于工作区；文档绿色：已add未commit，文档在暂存区有了关联记录；文档白色：已commit，文档在本地仓库区有了关联记录；文档蓝色：文档在本地仓库有关联记录，且在工作区有了变动。

+ git log --graph --pretty=oneline --abbrev-commit 查看分支及主干流程图

+ git 退出查看log：英文状态下按Q

+ git push的一般形式为 git push <远程主机名> <本地分支名>  <远程分支名> ，例如 git push origin master：refs/for/master
  1. git push origin master: <br>
  如果远程分支被省略，如上则表示将本地分支推送到与之存在追踪关系的远程分支（通常两者同名），如果该远程分支不存在，则会被新建。
  2. git push origin ：refs/for/master ：<br>
  如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支，等同于 git push origin --delete master
  3. git push origin：<br>
  如果当前分支与远程分支存在追踪关系，则本地分支和远程分支都可以省略，将当前分支推送到origin主机的对应分支。
  4. git push：<br>
  如果当前分支只有一个远程分支，那么主机名都可以省略，形如 git push，可以使用git branch -r ，查看远程的分支名
  5. git push -u origin master：<br>
  如果当前分支与多个主机存在追踪关系，则可以使用 -u 参数指定一个默认主机，这样后面就可以不加任何参数使用git push，
  不带任何参数的git push，默认只推送当前分支，这叫做simple方式，还有一种matching方式，会推送所有有对应的远程分支的本地分支，
  Git 2.0之前默认使用matching，现在改为simple方式。
  如果想更改设置，可以使用git config命令。git config --global push.default matching OR git config --global push.default simple；可以使用git config -l 查看配置
  6. git push --all origin：<br>
  当遇到这种情况就是不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要 -all 选项
  7. git push --force origin：<br>
  git push的时候需要本地先git pull更新到跟服务器版本一致，如果本地版本库比远程服务器上的低，那么一般会提示你git pull更新，如果一定要提交，那么可以使用这个命令。
  8. git push origin --tags：<br>
  git push 的时候不会推送分支，如果一定要推送标签的话那么可以使用这个命令

+ Git 中 HEAD、工作树和索引之间的区别
  1. 工作树/工作目录/工作空间是你看到和编辑的（源）文件的目录树。
  2. 索引/中转区（staging area）是个在 /.git/index，单一的、庞大的二进制文件，该文件列出了当前分支中所有文件的 SHA1 检验和、时间戳和文件名，它不是个带有文件副本的目录。
  3. HEAD是当前检出分支的最后一次提交的引用/指针。

+ Git 状态 untracked 和 not staged的区别
  1. untrack表示是新文件，没有被add过，是为跟踪的意思。
  2. not staged 表示add过的文件，即跟踪文件，再次修改没有add，就是没有暂存的意思

+ `git commit --amend`，修改注释

+ `git reset --soft HEAD^`，撤销最近的commit，HEAD~2，撤销最近两次commit。<br>
  `--mixed`：不删除工作空间改动代码，撤销commit，并且撤销`git add .` 操作这个为默认参数，`git reset --mixed HEAD^` 和 `git reset HEAD^` 效果是一样的。<br>
  `--soft`：不删除工作空间改动代码，撤销commit，不撤销`git add .` <br>
  `--hard`：删除工作空间改动代码，撤销commit，撤销`git add .` 注意完成这个操作后，就恢复到了上一次的commit状态。

+ git reset 参数

| 命令 | 作用 |
| :--- | :--- |
| `git reset HEAD` | 任何事情都不会发生，这是因为我们告诉GIT重置这个分支到HEAD，而这个正是它现在所在的位置(上图的3e07fd8位置)。 |
| `git reset HEAD~1	` | 意味着将HEAD从顶端的commit往下移动一个更早的commit |
| `git reset HEAD~2` | 意味着将HEAD从顶端的commit往下移动两个更早的commit |

| 命令 | 作用 |
| :--- | :--- |
| `soft` | –soft参数使git重置HEAD到另外一个commit。意味着工作区、暂存区都不会做任何变化，所有的在 HEAD和重置到的那个commit之间的所有变更集仍然在暂存区(index)区域中。 |
| `hard` | –hard参数将会blow out everything。它将重置HEAD到另外一个commit，重置缓存区以便反映HEAD的变化，并且重置工作区也使得其完全匹配起来。这是一个比较危险的操作⚠️，具有破坏性！ |
| `mixed(default）` | –mixed是reset的默认参数。它将重置HEAD到另外一个commit,并且重置缓存区。工作区不会被更改。所以所有从HEAD到你重置到的那个commit之间的所有变更仍然保存在工作区中，被标示为已变更 |

+ 查询某次历史提交的修改内容，首先`git log`显示历史的提交列表，然后`git show <commit-hashId>`便可以显示某次提交的修改内容；使用`git show <commit-hashId> filename`可以显示某次提交的某个内容的修改信息。

+ 删除某个全局配置项
  1. 查看Git所有配置：git config --list
  2. 删除全局配置项：
    1. 终端执行命令：git config --global --unset user.name
    2. 编辑配置文件：git config --global --edit
