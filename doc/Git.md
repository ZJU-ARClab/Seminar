
## Local 

初始化

```sh
git config --global user.name "github account name"
git config --global user.email "github account email"
git config --list
git init
```


提交
```sh
git add -A 全部提交到暂存区
git add . 不包括删除的 <filename> 指定的文件
git checkout . 从暂存区恢复所有 -- <filename> 指定的文件
git commit -m 在head后加一个节点
git commit -am  等于 git add . + git commit -m
git commit --amend 追加到前一次提交
```

分支
```sh
git branch -a 显示
git branch [branchx] 创建分支，不能用 HEAD 作为分支名
git branch -m [oldName]  [newName] 重命名分支
git checkout [nodex/branchx] 跳转 
git checkout -b [new branch name] [branchx] 复制并跳转
git checkout --orphan 创建空分支并复制最后提交的版本文件
git branch -d [branchx] 删除 merge 过的分支 -D 强制删除

git merge [branchx] 合并当前分支和另一分支，生成一个环
git merge [branchx] [branchy]

git rebase [branchx] 嫁接到其他分支上
git rebase [branchx] [branchy] y接到x上
git add -A && git rebase --continue 解决冲突并继续
git rebase --abort  还原
git gc 清除后不可复原
---master-x-x-mywork*

# 合并历史commits/修改注释
git rebase --interactive,-i [startpoint] [endpoint] 交互式, 前开后闭
git rebase -i HEAD~4
```

移动指针
```sh
HEAD 能指向：分支名，独立节点
git checkout [hash]
head^^ == master^^ == head~2
master^2 第二分叉
git commit 工作区node加到head后

分支名指向：节点
git branch -f [branchx] [nodex] 移动分支名
```

撤销
```sh
git reset [node]  当前branch移到[node],远程分支 git push -f
git reset --hard [node] 全改
git revert HEAD 追加一个node，这个node等于head^
git revert -n f7742cd..551c408 干掉 (f7742cd,551c408] 
```

提取
```sh
git cherry-pick [node1] [node2] ... 把这些node加到当前分支后,只有部分修改
git cherry-pick a1 a2 a3^
```

文件
```
git add
git rm
git checkout [branchx] -- [fileName]
```

解决冲突
```
git checkout [branchx]    HEAD 指向分支x
git reset --hard [nodey/branchy]  重置暂存区
git commit -m    提交到分支x
```

## Remote 

远程仓库
```sh
# 添加
git remote add <name> <url>    # git remote add origin https://github.com/xxx/xxx.git
git remote -v 显示
git remote show 详细信息
git remote remove 移除
git remote rename
# 新建推送 
git fetch 
git checkout origin/master -- README.md
git checkout origin/master -- LICENSE
git add -A 
git commit -m "init"
git push -u -f origin master:master
```

远程分支
```sh
git checkout origin/master
git commit xxx  没用，不会移动分支名
！本地缓存的远程分支在fetch时更新

git fetch 缓存所有远程分支
git merge origin/master == git pull 合并分支
git rebase origin/master == git pull --rebase 一条

git branch -r -D origin/master 删除本地的远程分支
```

push/fetch
```sh
git push origin local_branch:remote_branch 本地分支推到远程并跟新本地的远程缓存，只能追加否则会发生冲突
git push --force/-f     强制推送
git push --force-with-lease  更安全
git fetch origin remote_branch:local_branch

remote:a0-a1-a2
local:a0-a1-a3
solution1: git fetch; git rebase origin/master; git push
solution2: git fetch; git merge origin/master; git push
solution3: master 前移，new 分支，push new 


tips:
git fetch origin  :new_branch  新建分支
git push origin :master        删除远程master分支
```

追踪
```sh
git branch -u origin/master foo
git pull origin master 默认与当前分支合并
git pull origin remote_branch:local_branch 新建local_branch,合并到当前分支
```

解决远程历史冲突
```
git push -f
```