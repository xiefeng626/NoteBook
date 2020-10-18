# Git 笔记

## 远程仓库

> 从本地获取ssh公钥和密钥：ssh-keygen -t rsa -C "youremail@example.com"
>
> 给远程github设置sshkey 
>
> 创建远程仓库
>
> 关联远程仓库：git remote add origin git@github.com:用户名/项目
>
> 如：git@github.com:xiefeng626/basesStudy.git
>
> `git push -u origin master`第一次推送master分支（并关联）的所有内容；
>
> 克隆分支：
>
> git clone git@github.com:xiefeng626/basesStudy.git

## 分支关联

> + 远程不存在该分支：
>
> 本地推送到远程：git push -u origin develop(远程创建并推送并关联分支)
>
> + 远程存在该分支：
>
> git push --set-upstream origin newbranch 把本地分支和远程newbranch 分支关联

## 一个仓库可以关联多个远程

> git remote add origin git@github.com:用户名/项目
>
> 多加几个
>
> push和pull的时候加上 远程名：git push origin2

## git reset 和 git revert 的区别

> + reset
>
>   git reset的作用是修改HEAD的位置，即将HEAD指向的位置改变为之前存在的某个版本，如果想恢复到之前某个提交的版本，且那个版本之后提交的版本我们都不要了，就可以用这种方法。
>
>   即reset后目标版本之后的版本的修改都不见了
>
> + revet:反做
>
>   如果我们想撤销之前的某一版本，但是又想保留该目标版本后面的版本，记录下这整个版本变动流程，就可以用这种方法。
>
>   撤销之前的某一版本，但是又想保留该目标版本后面的版本，记录下这整个版本变动流程，就可以用这种方法。
>
>   即：往前前进了一个版本，过把以前的某个版本的修改回退了1。
