##git常用指令

    1.git初始化仓库
        git init
    2.git提交
        git add .
        git commit -m '提交的信息'
        git pull
        git push
    3.查看当前状态
        git status
    4.查看所有提交的log
        git reflog
    5.关联本地目录到远程库
        git remote add origin git@server-name:path/repo-name.git
    6.推送
        git push -u origin
        第一次推送master分支中所有内容，-u 参数是将本地的master分支推送到远程库中的master分支，
        且把本地的master分支和远程master分支关联起来，
        平时使用时如果有需要可以直接git push origin master就可以推送到远程库
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
        注：本地新建分支， push到远程服务器上之后，使用git pull或者git pull 拉取或提交数据时会报错，
        必须使用命令：git pull origin dev（指定远程分支）；
        如果想直接使用git pull或git push拉去提交数据就必须创建本地分支与远程分支的关联。
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
        git branch -D <branch_name> *试图删除一个分支时自己还没转移到另外的分支上，
        Git就会给出一个警告，并拒绝该删除操作。如果坚持要删除该分支的话，就需要在命令中使用-D选项(不建议使用)
    17.打tag
        1️⃣打印所有标签
            git tag
        2️⃣查看对应标签状态
            git checkout <版本号>
        3️⃣创建标签
            gti tag v1.0

            git tag <版本号>-light   创建轻量标签
            轻量标签指向一个发行版的分支，其只是一个像某commit的引用，不存储名称时间戳及标签说明等信息。
        4️⃣创建带附注标签
            git tag -a <版本号> -m "<备注信息>"
            相对于轻量标签，附注标签是一个独立的标签对象，包含了名称时间戳以及标签备注等信息，同时指向对应的commit。

            git tag -a <版本号> <SHA值> -m "<备注信息>"
            同时我们也可以像特定的commit添加标签，使用该commit对应的SHA值即可
        5️⃣删除本地标签
            git tag -d <版本号>
        6️⃣将本地标签提交到远程仓库
            git push origin --tags   推送所有标签

            git push origin <版本号>   推送指定版本的标签
        7️⃣删除远程仓库的标签
            git push origin --delete <版本号>  新版本Git (> v1.7.0)
            同创建本地标签一样，删除了本地标签之后也要同时删除远程仓库的标签。

            git push origin :refs/tags/<版本号>
            旧版本Git并没有提供直接删除的方法，而我们可以通过将一个空标签替换现有标签来实现删除标签
    18.代码回滚
        https://blog.csdn.net/ligang2585116/article/details/71094887
        1️⃣在未进行git push前的所有操作，都是在“本地仓库”中执行的。我们暂且将“本地仓库”的代码还原操作叫做“撤销”！
            情况一：文件被修改了，但未执行git add操作(working tree内撤销) 
                git checkout fileName
                git checkout .
            情况二：同时对多个文件执行了git add操作，但本次只想提交其中一部分文件
                git add *
                git status
                # 取消暂存
                git reset HEAD <filename>
            情况三：文件执行了git add操作，但想撤销对其的修改（index内回滚）
                # 取消暂存
                git reset HEAD fileName
                # 撤销修改
                git checkout fileName
            情况四：修改的文件已被git commit，但想再次修改不再产生新的Commit
                # 修改最后一次提交 
                git add sample.txt
                git commit --amend -m"说明"
            情况五：已在本地进行了多次git commit操作，现在想撤销到其中某次Commit
                git reset [--hard|soft|mixed|merge|keep] [commit|HEAD]
                