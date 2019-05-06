---
title: git 入门
date:  2019-05-06 12:00:00
tags: [git]
categories: 张永枫
description: git 入门
---

<!-- TOC -->

[随手记](#随手记)

[安装](#安装)

[配置用户名、邮箱](#配置用户名、邮箱)

[创建版本库](#创建版本库)

[把文件添加到版本库(暂存区)](#把文件添加到版本库暂存区)

[提交到本地代码库](#提交到本地代码库)

[仓库当前的状态](#仓库当前的状态)

[git status小结](#gitstatus小结)

[对比文件修改了什么内容](#对比文件修改了什么内容)

[查看提交的日志](#查看提交的日志)

[回退到上一个版本](#回退到上一个版本)

[查看命令历史](#查看命令历史)

[撤销修改](#撤销修改)

[提交到远程代码库](#提交到远程代码库)

[关联远程库](#关联远程库)

[创建SSH_Key](#创建ssh_key)

[查看所有分支](#查看所有分支)

[切换分支](#切换分支)

[合并分支](#合并分支)

[删除掉dev分支](#删除掉dev分支)

[分支小结](#分支小结)

[解决冲突](#解决冲突)

[分支管理策略](#分支管理策略)

[强行删除分支](#强行删除分支)

[多人协作](#多人协作)

[更新远程库的代码到本地](#更新远程库的代码到本地)

[添加标签](#添加标签)

[操作标签](#操作标签)

[查看远程库的信息](#查看远程库的信息)

[删除已关联的名为origin的远程库](#删除已关联的名为origin的远程库)

[忽略特殊文件](#忽略特殊文件)

[强制添加忽略的文件](#强制添加忽略的文件)

[检查添加文件是否被忽略](#检查添加文件是否被忽略)

[设置命令别名](#设置命令别名)

[配置文件](#配置文件)


***
## 随手记 
    1、分布式版本控制系统
    记录每次文件的改动，并且可以协作编辑
    
## 1、基本操作
[目录](#git)
### 安装
    // Debian/Ubuntu Linux 
    sudo apt-get install git
    
    // 其他linux版本，源码安装
    git官网 https://git-scm.com/
    下载源码，然后解压，依次输入
    ./config 
    make
    sudo make install
    
    //mac osx 
    通过homebrew安装 
    homebrew官网: http://brew.sh
[目录](#git)
### 配置用户名、邮箱 
    git config --global user.name zhangyongfeng1
    
    git config --global user.username zhangyongfeng1
    //配置用户名
    
    git config --global user.email 503977995@qq.com
    //配置邮箱
    
    git config --global user.name
    //没有传参数时，查询当前配置的用户名
[目录](#git)
### 创建版本库 

    ubuntu:~/environment $   mkdir learngit
    ubuntu:~/environment $     cd learngit
    ubuntu:~/environment/learngit $     pwd
    /home/ubuntu/environment/learngit
    ubuntu:~/environment/learngit $ git init
    Initialized empty Git repository in /home/ubuntu/environment/learngit/.git/
    ubuntu:~/environment/learngit (master) $ ls -al
    total 12
    drwxrwxr-x 3 ubuntu ubuntu 4096 Apr 26 06:02 .
    drwxr-xr-x 6 ubuntu ubuntu 4096 Apr 26 06:00 ..
    drwxrwxr-x 7 ubuntu ubuntu 4096 Apr 26 06:02 .git
[目录](#git)       
### 把文件添加到版本库暂存区
    
    // 添加文件
    git add <file>
    //在learngit目录下新建 一个文件readme.md
    git add readmne.md
    git add . 
    //当前目录下的文件全部提交
[目录](#git) 
### 提交到本地代码库
    git commit -m <message>
    git commit -m 注解信息
[目录](#git)   
### 仓库当前的状态 
    git status
    
    On branch master
    nothing to commit, working tree clean
    //工作目录是干净的

    On branch master
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

    modified: readme.txt
[目录](#git)    
### gitstatus小结
    要随时掌握工作区的状态，使用git status命令。
    如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
[目录](#git)    
### 对比文件修改了什么内容 
    git diff <filename>
    
    $ git diff readme.txt 
    diff --git a/readme.txt b/readme.txt
    index 46d49bf..9247db6 100644
    --- a/readme.txt
    +++ b/readme.txt
    @@ -1,2 +1,2 @@
    -Git is a version control system.
    +Git is a distributed version control system.
    Git is free software.
 [目录](#git)    
### 查看提交的日志
    git log
    
    git log --pretty=oneline
[目录](#git)    
### 回退到上一个版本 
    get reset
    HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，
    使用命令git reset --hard commit_id。
   
    
    在Git中，用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
    
    git reset --hard HEAD^ 
    //回退到上一个版本
    
    git reset --hard 772a2f
    //回到指定的版本号 
    
[目录](#git)   
### 查看命令历史 

    git reflog

    用来记录你的每一次命令：
[目录](#git)
### 撤销修改 
    场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
    
    场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
    
    场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
[目录](#git)
### 提交到远程代码库 
    
    git push 
    
    git push origin master
[目录](#git)    
### 关联远程库 

    要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；

    关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

    此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
[目录](#git)   
### 创建ssh_key
    由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：

    第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

    $ ssh-keygen -t rsa -C "youremail@example.com"
    你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

    如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

    第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

    然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

    github-addkey-1

    点“Add Key”，你就应该看到已经添加的Key：

    github-addkey-2
[目录](#git)
### 查看所有分支 
    git branch 
    创建分支：git branch <name>
    git branch命令会列出所有分支，当前分支前面会标一个*号。
[目录](#git)
### 切换分支 
    git checkout 分支名 
    git checkout master 
[目录](#git)   
### 合并分支 
    git merge dev
    
[目录](#git) 
### 删除掉dev分支 
    git branch -d dev 

    Deleted branch dev (was b17d20e).
    删除后，查看branch，就只剩下master分支了：
    git branch
    因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。

[目录](#git)
### 分支小结 

    Git鼓励大量使用分支：
    
    查看分支：git branch
    
    创建分支：git branch <name>
    
    切换分支：git checkout <name>
    
    创建+切换分支：git checkout -b <name>
    
    合并某分支到当前分支：git merge <name>
    
    删除分支：git branch -d <name>
[目录](#git)
### 解决冲突 
    主线和分支修改的文件一样时，合并之后会报文件有冲突
    
    用带参数的git log也可以看到分支的合并情况：
    git log --graph --pretty=oneline --abbrev-commit -10
    
    当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

    解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

    用git log --graph命令可以看到分支合并图。
[目录](#git)
### 分支管理策略 
    
    通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。

    如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
[目录](#git)
### 强行删除分支 
    git branch -D feature-vulcan
    
[目录](#git)
### 多人协作 
    多人协作的工作模式通常是这样：
    
    首先，可以试图用git push origin <branch-name>推送自己的修改；
    
    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
    
    如果合并有冲突，则解决冲突，并在本地提交；
    
    没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
    
    如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
    
    这就是多人协作的工作模式，一旦熟悉了，就非常简单。
[目录](#git)   
### 更新远程库的代码到本地 
    git pull
    
    查看远程库信息，使用git remote -v；

    本地新建的分支如果不推送到远程，对其他人就是不可见的；
    
    从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
    
    在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
    
    建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
    
    从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。
[目录](#git)   
### 添加标签
    命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
    
    命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；
    
    命令git tag可以查看所有标签。
[目录](#git)    
### 操作标签 
    git tag -d v0.1
    
    小结
    命令git push origin <tagname>可以推送一个本地标签；
    
    命令git push origin --tags可以推送全部未推送过的本地标签；
    
    命令git tag -d <tagname>可以删除一个本地标签；
    
    命令git push origin :refs/tags/<tagname>可以删除一个远程标签。
[目录](#git)
### 查看远程库的信息 
    git remote
    
    查看更多的信息
    git remote -v
[目录](#git)    
### 删除已关联的名为origin的远程库 
    git remote rm origin
    先关联GitHub的远程库：

    git remote add github git@github.com:michaelliao/learngit.git
    注意，远程库的名称叫github，不叫origin了。
    
    接着，再关联码云的远程库：
    
    git remote add gitee git@gitee.com:liaoxuefeng/learngit.git
    同样注意，远程库的名称叫gitee，不叫origin。
    
    现在，我们用git remote -v查看远程库信息，可以看到两个远程库：
    
    git remote -v
    gitee    git@gitee.com:liaoxuefeng/learngit.git (fetch)
    gitee    git@gitee.com:liaoxuefeng/learngit.git (push)
    github    git@github.com:michaelliao/learngit.git (fetch)
    github    git@github.com:michaelliao/learngit.git (push)
    如果要推送到GitHub，使用命令：
    
    git push github master
    如果要推送到码云，使用命令：
    
    git push gitee master
    这样一来，我们的本地库就可以同时与多个远程库互相同步：
[目录](#git)
### 忽略特殊文件 
    .gitignore
[目录](#git)
### 强制添加忽略的文件 
    git add -f App.class
[目录](#git)
### 检查添加文件是否被忽略 
    git check-ignore -v App.class
    
[目录](#git)
### 设置命令别名 
    git config --global alias.st status
    //状态
    git config --global alias.co checkout
    //更新
    git config --global alias.ci commit
    //提交
    git config --global alias.br branch
    //分支
    
    git config --global alias.unstage 'reset HEAD'
    //命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区。既然是一个unstage操作，就可以配置一个unstage别名：
    
    git unstage test.py
    =git reset HEAD test.py
    
    git config --global alias.last 'log -1'
    //配置一个git last，让其显示最后一次提交信息
    git last
    
    git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
 [目录](#git)   
## 配置文件 

    .git/config
    
    cat ./git/config
    
[搭建见廖老师教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137583770360579bc4b458f044ce7afed3df579123eca000)