##git常用指令

    1.git初始化仓库
        git init
    2.git提交
        git add .
        git commit -m '提交的信息'
        git push
    3.查看当前状态
        git status
    4.查看所有提交的log
        git reflog
    5.关联本地目录到远程库
        git remote add origin git@server-name:path/repo-name.git
    6.推送
        git push -u origin
        第一次推送master分支中所有内容，-u 参数是将本地的master分支推送到远程库中的master分支，且把本地的master分支和远程master分支关联起来，以后可以*平时使用时如果有需要可以直接git push origin master就可以推送到远程库
    7.查看分支
        git branch
        -a 查看所有分支
    8.新建本地分支
        git branch 分支名
        git checkout -b 分支名 
            --创建本地分支并切换
    9.切换本地分支
        git checkout 分支名
    10.推送本地分支
        git push origin 本地分支名
    11.新建本地分支与远程分支关联
        git branch –-set-upstream 本地新建分支名 origin/远程分支名(可能已经不支持)
        git push --set-upstream origin dev（可以用）
        注：本地新建分支， push到远程服务器上之后，使用git pull或者git pull 拉取或提交数据时会报错，必须使用命令：git pull origin dev（指定远程分支）；如果想直接使用git pull或git push拉去提交数据就必须创建本地分支与远程分支的关联。
    12.查看本地分支和远程分支的跟踪关系
        git branch -vv
    13.在远程分支的基础上建立develop分支，并且让develop分支追踪origin/develop远程分支。
        git checkout -b develop origin/develop
    14.暂存临时代码
        git stash *暂存代码，推入git栈中，
        git stash apply  *取出暂存的代码
        git stash list *将当前的Git栈信息打印出来，找到对应的版本号,git stash apply 版本号 来取出对应版本。
        git stash clear *将git栈清空
    15.合并代码
        git merge dev *此处是合并dev到master分支（当前分支master）
    16.删除分支
        git branch -d dev *删除的分支不是当前正在打开的分支，使用branch -d直接删除
        git branch -D <branch_name> *试图删除一个分支时自己还没转移到另外的分支上，Git就会给出一个警告，并拒绝该删除操作。如果坚持要删除该分支的话，就需要在命令中使用-D选项(不建议使用)
    17.
