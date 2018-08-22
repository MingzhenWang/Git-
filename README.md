# Git-
# Git命令整理集合

## 1. Git基础

### 1.1 获取Git仓库

#### 1.1.1 在现有目录中初始化仓库

* git init  ——初始化现有目录


#### 1.1.2 克隆现有的仓库

* git clone [url] ——克隆仓库  

* git clone [url] repository_name ——克隆远程仓库，并自定义本地仓库的名字  

### 1.2 记录每次更新到仓库  

* git status ——检查当前文件状态  

* echo ‘my project’ README ——当前目录创建文件并写入  

* git add 文件名 ——暂存已修改文件  

* git add * ——全部暂存

* git status -s/--short ——状态简览  
新添加的未跟踪文件前面有 ?? 标记，新添加到暂存区中的文件前面有 A 标记，修改过的文件前面有 M 标记。出现在右边的 M 表示该文件被修改了但是还没放入暂存区，出现在靠左边的 M 表示该文件被修改了并放入了暂存区。    

* touch .gitignore ——创建忽略文件  

* cat .gitignore ——查看忽略文件  

* git diff ——查看未暂存的文件更新了哪些部分  

* git diff --staged/--cached ——查看已暂存未提交的内容  

* git difftool ——用 Araxis、emerge、vimdiff 等软件输出 diff 分析结果
 
* git difftool --tool-help ——查看系统支持哪些 GitDiff 插件  

* git commit ——提交更新    

* git commit -m 'first change' ——提交更新并提交消息 

* git commit -a -m 'first change' ——直接暂存并提交   

* git rm ——从当前跟踪列表移除文件，并从当前目录删除  

* git rm -f/--force ——用于防止误删还没有添加到快照的数据

* git rm --cached ——仅在暂存区删除，保留文件在当前目录    

* git rm log/\*.log ——删除log/ 目录下扩展名为 .log 的所有文件  
* git rm \*~ ——删除以 ~ 结尾的所有文件  

* git mv file_from file_to ——重命名file_from  

### 1.3 查看提交历史  

* git log ——按提交时间列出所有的更新的详细内容（查看提交历史）

```
    -p ——按补丁格式显示每个更新之间的差异
    -p -2 ——仅显示最近两次提交

    --stat ——显示每次更新的文件修改统计信息  
    --shortstat ——只显示--stat中最后的行数修改添加移除统计

    --name-only ——仅在提交信息后显示已修改的文件清单
    --name-status ——显示新增、修改、删除的文件清单

    --abbrev-commit ——仅显示SHA-1的前几个字符，非所有的40个字符

    --relative-date 使用较短的相对时间显示，比如“2 weeks ago”

    --pretty=oneline ——将每个提交放在一行,提交数
    --pretty=oneline --graph ——显示ASCII图形表示的分支合并历史

    --pretty=short ——展示的信息最少
    --pretty=full ——展示的信息量居中
    --pretty=fuller ——展示的信息最多

    --pretty=format:"%h-%an" ——定制要显示的记录格式
    --pretty=format:"%h %s" --graph ——显示 ASCII 图形表示的分支合并历史
```

* 限制git log 输出

```
    -<n> —— n可以是任何整数，表示仅显示最近的若干条提交

    --since=2.weeks, --after="2008-10-01" ——仅显示指定时间之后的提交
    --until, --before ——仅显示指定时间之前的提交

    --author ——仅显示指定作者相关的提交
    --grep ——仅显示含指定关键字的提交
    (注：如果要得到同时满足这两个选项搜索条件的提交，就必须用  --all-match 选项。否则，满足任意一个条件的提交都会被匹配出来)

    --committer 仅显示指定提交者相关的提交

    -S ——仅显示添加或移除了某个关键字的提交
    如：git log -Sfunction_name，
    找出添加或移除了某一个特定函数的引用的提交

```  

### 1.4 撤销操作  

* git commit --amend ——重新提交，编辑后保存会覆盖原来的提交信息  

* git reset HEAD < file> ——取消暂存的文件

* git reset Head --hard < file> ——可能导致工作目录中所有当前进度丢失  

* git checkout -- < file> ——撤销对文件的修改  

### 远程仓库的使用  

* git remote ——查看已配置的远程仓库服务器，如果你已经克隆了自己的仓库，那么至少应该能看到 origin，这是 Git 给你克隆的仓库服务器的默认名  

* git remote -v ——-v显示需要读写远程仓库使用的Git保存的简写与其对应的 URL  

* git remote add < shortname> < url> 添加一个新的远程 Git 仓库，同时指定一个可以轻松引用的简写  

* git fetch [remote-name] ——从远程仓库中获得数据，会将数据拉取到你的本地仓库，但它并不会自动合并或修改你当前的工作。  

* git pull ——会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支  

* git push [remote-name] [branchname] ——推送到远程仓库，本地分支推送到远程服务器  

* git remote show [remote-name] ——查看远程仓库  

* git remote rename pb paul ——远程仓库重命名，将pb改为Paul  

* git remote rm ——移除远程仓库  

### 1.5 打标签  

* git tag ——列出标签  

* git tag -l 'v1.8.5*' ——列出1.8.5系列标签  

* git tag -a v1.4 -m 'my version 1.4' ——创建附注标签  

* git show v1.4 ——显示标签信息与对应的提交信息  

* git tag v1.4-lw ——创建轻量标签  

* git show 轻量标签 ——只有提交信息，没有标签信息  

* git tag -a v1.2 9fceb02 ——后期加标签，末尾指定（部分）校验和  
* git push origin [tagname] ——共享标签，推送到共享服务器  

* git push origin --tags ——把不在远程服务器上的标签全部推送  
 
* git checkout -b [branchname] [tagname] ——检出标签，在特定的标签上创建一个新分支  

### 1.6 Git别名  

* 如果不想每次都输入完整的 Git 命令，可以通过 git config 文件来轻松地为每一个命令设置一个别名  

* git config --global alias.co checkout -git checkout=git co
* git config --global alias.br branch - git branch=git br
* git config --global alias.ci commit - git commit=git ci
* git config --global alias.st status - git status=git st  

* git config --global alias.unstage 'reset HEAD --' ——解决取消暂存文件的易用性问题，向Git 中添加自己的取消暂存别名。  

* git config --global alias.last 'log -1 HEAD' —— 查看最后一次提交  

* 若要执行外部命令，而不是一个Git子命令，可以在命令前面加入!符号  
* git config --global alias.visual '!gitk' ——自己写一些与Git 仓库协作的工具的话


## 2. git分支

* git branch branch_name  ——创建分支

* git log ——查看各个分支当前所指对象

* git log --oneline --decorate ——

* git checkout branch_name ——分支切换  

* git log --oneline --decorate --graph --all  
输出你的提交历史、各个分支的指向以及项目的分支分叉情况  

* git checkout -b branch_name ——新建并切换分支  

* git checkout master ——切换分支
* git merge hotfix ——将hotfix分支融合到master分支  

* git branch -d hotfix ——分支融合之后，删除hotfix分支  

* git branch ——显示当前所有分支  

* git branch -v ——查看每一个分支的最后一次提交  

* git branch --merged ——查看已经合并到当前分支的分支  

* git branch --no-merged ——尚未合并到当前分支的分支  

* git branch -D testing ——强制删除尚未合并的分支  


