1. `git log -p -2`，-p用来显示每次提交的内容差异，也可以加上 -2 来仅显示最近两次提交，不过实践中我们是不太用这个选项的，Git 在输出所有提交时会自动调用分页程序，所以你一次只会看到一页的内容。
2. `git log --stat`，显示每次提交的简略的统计信息，即：列出所有被修改过的文件、有多少文件被修改了以及被修改过的文件的哪些行被移除或是添加了。
3. `git log --pretty=oneline`，--pretty用以指定使用不同于默认格式的方式展示提交历史，这个选项有一些内建的子选项供你使用。 比如用 oneline 将每个提交放在一行显示，另外还有 `short`，`full` 和 `fuller`。
4. `git log --pretty=format:"%h - %an, %ar : %s"`，指定格式显示：

**Table1: `git log --pretty=format`常用选项**

| 选项 | 说明 |
| :--- | :--- |
| `%H` | 提交对象id（commit id）的完整哈希字串 |
| `%h` | 提交对象的简短哈希字串 |
| `%T` | 树对象（tree）的完整哈希字串 |
| `%t` | 树对象的简短哈希字串 |
| `%P` | 父对象（parent）的完整哈希字串 |
| `%p` | 父对象的简短哈希字串 |
| `%an` | 作者（author）的名字 |
| `%ae` | 作者的电子邮件地址 |
| `%ad` | 作者修订日期（可以用 `--date=` 选项定制格式） |
| `%ar` | 作者修订日期，按多久以前的方式显示 |
| `%cn` | 提交者（committer）的名字 |
| `%ce` | 提交者的电子邮件地址 |
| `%cd` | 提交日期 |
| `%cr` | 提交日期，按多久以前的方式显示 |
| `%s` | 提交说明 |

**Table2: `git log`常用选项**

| 选项 | 说明 |
| :--- | :--- |
| `-p` | 按补丁格式显示每个更新之间的差异 |
| `--stat` | 显示每次更新的文件修改统计信息 |
| `--shortstat` | 只显示 --stat 中最后的行数修改添加移除统计 |
| `--name-only` | 仅在提交信息后显示已修改的文件清单 |
| `--name-status` | 显示新增、修改、删除的文件清单 |
| `--abbrev-commit` | 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符 |
| `--relative-date` | 使用较短的相对时间显示（比如，“2 weeks ago”） |
| `--graph` | 显示 ASCII 图形表示的分支合并历史 |
| `--pretty` | 使用其他格式显示历史提交信息。可用的选项包括 `oneline`，`short`，`full`，`fuller` 和 `format`（后跟指定格式） |

5. `git log --since（或after）=2.weeks`，仅显示指定时间之后的提交，这个命令可以在多种格式下工作，比如说具体的某一天 "2008-01-15"，或者是相对地多久以前 "2 years 1 day 3 minutes ago"。
6. `git log --until（或before）`，仅显示指定时间之前的提交，与`since`同时使用表示时间段，例如：`git log --after="2014-7-1" --before="2014-7-4"`。
7. `git log <since>..<until>`，这个命令可以查看某个范围的commit
8. `git log --author="John"`，显示指定作者的提交。
9. `git log --grep="JRA-224:"`，搜索提交说明中的关键字，可以传入-i用来忽略大小写，如果想同时使用--grep和--author，必须在附加一个--all-match参数。
10. `git log -- foo.py bar.py`，按文件筛选，`--` 告诉 `git log` 接下来的参数是文件路径而不是分支名。如果分支名和文件名不可能冲突，你可以省略 `--`。
11. 如果同时使用两个筛选条件，要得到同时满足这两个选项搜索条件的提交，就必须用 `--all-match` 选项，否则，满足任意一个条件的提交都会被匹配出来。
12. `git log file/` 查看file文件夹下所有文件的提交记录
13. `git log -S"<string>"、-G"<string>"`，有时你想搜索和新增或删除某行代码相关的commit. 可以使用这条命令，例如：你想知道Hello, World!这句话是什么时候加入到项目里去的，可以用：`git log -S"Hello,World!"`，如果你想使用正则表达式去匹配而不是字符串, 那么你可以使用`-G`代替`-S`
14. `git log <since>..<until>`，这个命令可以查看某个范围的commit，当使用`branch`做为`range`参数的时候. 能很方便的显示2个`branch`之间的不同，比如：`git log master..feature`，`master..feature`这个范围包含了在`feature`有而在`master`没有的所有`commit`，同样，如果是`feature..master`包含所有`master`有但是`feature`没有的`commit`。<br>
如果是三个点，表示或的意思：`git log master...test` 查询`master`或`test`分支中的提交记录。

**Table3: 限制`git log`输出的选项**

| 选项 | 说明 |
| :--- | :--- |
| `-(n)` | 仅显示最近的 n 条提交 |
| `--since`, `--after` | 仅显示指定时间之后的提交 |
| `--until`, `--before` | 仅显示指定时间之前的提交 |
| `--author` | 仅显示指定作者相关的提交 |
| `--committer` | 仅显示指定提交者相关的提交 |
| `--grep` | 仅显示含指定关键字的提交 |
| `-S` | 仅显示添加或移除了某个关键字的提交 |
