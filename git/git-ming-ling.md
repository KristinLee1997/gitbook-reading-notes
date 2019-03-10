# GIT命令

which git ：查看git目录

**获得版本库** git init:创建git仓库 git clone:将远程版本库中项目复制一份到本地

**版本管理** git add:将已修改文件纳入暂存区 git commit：将暂存区文件存入工作区 git commit -m "备注信息” git commit --amend -m '修正commit message' git rm：删除版本库中多余的文件

**查看信息** git help:git help config git config --help man git-config git log git log:空格查看以前的log， q退出， ctrl+f往前， ctrl+b往回 git -n:显示最近的n行 git log --pretty=oneline:以一行形式显示日志 git log --pretty=format"%h-%an,%ar:%s":定制格式 git diff

**远程协作** git pull：将远程版本库中文件拉取到本地 git push：将本地文件推送到远程版本库 git status：查看当前文件状态

**对于user.name和user.email来说，有3个地方可以设置** 1./etc/gitconfig\(对于整个系统的，几乎不会使用\)优先级低 git config --system 2.~/.gitconfig\(针对于所有git项目，很常用\)优先级中 git config --global 3.git/config（针对于特定项目）优先级高 git config --local

git config --local user.name 'krisitn' git config --local --unset user.name git config --list

git checkout -- text.txt：删除暂存区中对text.txt文件的修改,恢复到修改之前 git rm --cache 文件：表示将文件从暂存区中删除 git reset HEAD test.txt:表示将文件从暂存区中删除 git rm “test.txt”:删除一个文件，将被删除的文件纳入暂存区

echo "hello world" &gt; test.txt:将“hello world”保存到test.txt文件中 ctrl+a：快速到一行命令最左端 ctrl+e：快速到一行命令最右端

git mv test.txt test2.txt: 将test.txt重命名



git status: 查看当前状态 git log：显示提交信息 git rm xxx.txt: 删除xxx文件 git rm: 删除一个文件；将被删除的文件纳入暂存区 git mv：将当前文件一定到另一个目录 HEAD：指向当前分支，在.git/HEAD中记录

**恢复删除已经add到缓存区的文件：** 删除：git rm test.txt git commit -am "delete test.txt" 恢复： git reset HEAD test.txt 将待删除的文件从暂存区恢复到工作区 git checkout -- ‘reset text’ 将工作区中的修改丢弃掉 git commit -am "delete test.txt"

删除： rm test.txt git commit -am "delete test.txt" 恢复： git checkout -- ‘reset text’ git add test.txt git commit -am "delete test.txt"

**重命名文件名称：** 重命名： git mv test.txt test2.txt 将test文件重命名为test2 恢复： git reset HEAD test2.txt git checkout -- test2 git checkout -- test rm test2.txt

重命名： mv test.txt test2.txt git add test.txt test2.txt

**修改提交的comment：** git commit --amend -m "再次修正comment信息"

**查看日志：** git log -2：查看最近两条提交记录 git log --pretty-oneline git log --pretty=format:"%h - %an, %ar : %s" git log —graph:以图形方式展示log git reflog：查看操作日志

**查看git帮助** git help config git config --help man git-config

**创建分支** git branch xxx：创建xxx分支 git branch -v：查看最近一次的提交

**切换分支** git checkout xxx:切换到xxx分支 git checkout -b xxx:创建并切换到xxx分支

**删除分支** git branch -d xxx:删除xxx分支，但是如果该分支存在需要merge的文件，需要先merge再删除 git branch -D xxx:强制删除xxx分支

**合并分支** git merge test:将test分支合并到当前分支

**merge时禁用fast-forward** git merge —no-ff:merge时禁用fast-forward

**git版本回退** 版本回退 git reset —hard HEAD^:回退到上一个版本 git reset —hard HEAD~3:回退到三次提交之前 git reset —hard commitid:回退到某一具体id

git checkout —test.txt: 丢掉相对于暂存区中最后一次添加的文件内容所做的变更 git reset HEAD test.txt：

