#Git学习笔记
2013/12/20
##Git在Windows上配置SSH公钥
###一、安装git
1. [下载最新版](http://git-scm.com/download/win)
1. 第一项选Run Git from the Windows Command Prompt
1. 第二项选Use OpenSSH
1. 第三项选Chechout as-is,commit as-is

###二、设置git的user name和email：
    $ git config --global user.name "jeremylam" 
    $ git config --global user.email "jeremylam14@gmail.com"

###三、生成密钥
运行Git Bash

	ssh-keygen -t rsa -C “jeremylam14@gmail.com”
按3个回车，密码为空。（不要输密码）  
然后到.ssh下面将id_rsa.pub里的内容复制出来粘贴到github个人中心的ssh key里面。

完成！

##Bitbucket
###克隆新分支
如果您尚未设置，请在您的电脑上设置 Git。

	mkdir /path/to/your/project
	cd /path/to/your/project
	git init
	git remote add origin ssh://git@bitbucket.org/jeremylam/av.web.git
访问[Bitbucket 101](https://confluence.atlassian.com/x/cgozDQ?utm_source=internal&utm_medium=link&utm_campaign=blank_repo) 获取更多关于设置的帮助信息。
###导入一个已有的仓库
您在计算机上已经有了一个Git仓库。让我们把它发布到Bitbucket。

	cd /path/to/my/repo
	git remote add origin ssh://git@bitbucket.org/jeremylam/av.web.git
	git push -u origin --all # pushes up the repo and its refs for the first time
	git push -u origin --tags # pushes up any tags

你想从另一个网站抓取一个版本库吗？试试我们的导入功能！
###修改并推送
每个项目都需要一个 README 文件。 你的 README 会出现在项目首页，向你的访客解释你的项目是做些什么的。

	echo "# This is my README" >> README.md
	git add README.md
	git commit -m "First commit. Adding a README."
	git push -u origin master
##GitHub
###Create a new repository on the command line
	touch README.md
	git init
	git add README.md
	git commit -m "first commit"
	git remote add origin git@github.com:jeremylam/Python-Tricks.git
	git push -u origin master
###Push an existing repository from the command line
	git remote add origin git@github.com:jeremylam/Python-Tricks.git
	git push -u origin master
##常用命令
###Git配置
    git config --global color.ui true
    git config --global alias.co checkout  # 设置别名
    git config --global alias.ci commit
    git config --global alias.st status
    git config --global alias.br branch
    git config -1  # 列举所有配置

###查看、添加、提交、删除、找回，重置修改文件
	git init  # 将在当前目录创建一个隐藏的名为".git"的目录。
	git init project1  # 等价于 $ mkdir project1 && cd project1 && git init
	
	git status  # 查看当前状态  
    
	git help <command>  # 显示command的help
    git show  # 显示某次提交的内容
    git show $id
    
	git checkout -- <file>   # 抛弃工作区修改
    git checkout .   # 抛弃工作区修改
    
	git add <file>  # 将工作文件修改提交到本地暂存区
    git add .   # 将所有修改过的工作文件提交暂存区
    
	git rm <file>  # 从版本库中删除文件
    git rm <file> --cached  # 从版本库中删除文件，但不删除文件

    git reset <file># 从暂存区恢复到工作文件
    git reset -- .  # 从暂存区恢复到工作文件
    git reset --hard# 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改

    git commit <file>
    git commit .
    git commit -a   # 将git add, git rm和git ci等操作都合并在一起做
    git commit -am "some comments"
    git commit --amend  # 修改最后一次提交记录

    git revert <$id># 恢复某次提交的状态，恢复动作本身也创建了一次提交对象
    git revert HEAD # 恢复最后一次提交的状态
    