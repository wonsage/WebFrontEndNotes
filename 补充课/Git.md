**git add -A&git add .**

git add -A 提交所有变化

git add -u 提交被修改(modified)和被删除(deleted)文件，不包括新文件(new)

git add . 提交新文件(new)和被修改(modified)文件，不包括被删除(deleted)文件

# 合并 git rebase、git merge
**rebase 重定基地，重新设立起点**

都是将一个分支的更改并入另一个分支，只不过方式不同

  

## git merge
将当前分支合并到指定分支
## git rebase
将当前分支移植到指定分支或指定commit上

`git rebase -i <commit>`

`git rebase --continue` 解决冲突后，继续rebase

  

## 区别

### merge
通过其合并分支会新增一个merge commit，再将两个分支历史联系起来。
非破坏性的操作，对现有分支不会有更改，历史记录相对复杂。
### rebase
将整个分支移动到另一个分支上，有效整合所有分支的提交。

历史记录清晰，消除了git merge所需的不必要的合并提交。

**git reset 和 git revert**

**git reset重置**

执行遗弃时，需要根据影响的范围而指定不同的参数，可以指定是否复原索引或工作树内容

**git revert恢复**

在当前提交后面，新增一次提交，抵消掉上一次提交导致的所有变化，不会改变过去的历史，主要是用于安全地取消过去发布的提交

此次操作之前和之后的 commit和history都会保留，并且把这次撤销，作为一次最新的提交，如下：

撤销（revert）被设计为撤销公开的提交（比如已经push）的安全方式，git reset被设计为重设本地更改

重设完全地移除了一堆更改，而撤销保留了原来的更改，用一个新的提交来实现撤销

两者主要区别如下：

- git revert是用一次新的commit来回滚之前的commit，git reset是直接删除指定的commit
- git reset 是把HEAD向后移动了一下，而git revert是HEAD继续前进，只是新的commit的内容和要revert的内容正好相反，能够抵消要被revert的内容
- 在回滚这一操作上看，效果差不多。但是在日后继续 merge 以前的老版本时有区别

> git revert是用一次逆向的commit“中和”之前的提交，因此日后合并老的branch时，之前提交合并的代码仍然存在，导致不能够重新合并

> 但是git reset是之间把某些commit在某个branch上删除，因而和老的branch再次merge时，这些被回滚的commit应该还会被引入

- 如果回退分支的代码以后还需要的情况则使用git revert， 如果分支是提错了没用的并且不想让别人发现这些错误代码，则使用git reset
# 切换 checkout switch
### checkout
可以用来切换分支和恢复修改。
### switch
[Git - git-switch Documentation (git-scm.com)](https://git-scm.com/docs/git-switch/zh_HANS-CN)
`git switch <branch>` 
`git switch -c <branch>` 新建分支，然后切换至新分支
2.23版本新增了switch方法和restore，分别用于切换分支和恢复修改，这样一定程度上替代了checkout命令，但checkout仍被保留。