## Git常用操作

### 1. git 操作流程图

![](..//images/git/git使用命令.png)

### 2. 创建仓库

```shell
git init    #在当前目录创建一个git仓库
git init [project-name]  #新建一个目录，将其初始化为git代码库
git clone [url] #下载一个远程仓库代码到本地仓库
```

### 3. 代码添加到暂存区

```shell
$ git add [file1] [file2] ... # 添加多个指定文件到暂存区
$ git add [dir]               # 添加指定目录到暂存区，包括子目录
$ git add .                   # 添加当前目录的所有文件到暂存区
```

### 4. 代码提交到本地仓库

```shell
$ git commit -m [message]                     # 提交暂存区所有文件到仓库区
$ git commit [file1] [file2] ... -m [message] # 提交暂存区的指定文件到仓库区
$ git commit -a                               # 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -v                               # 提交时显示所有diff信息
# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]
# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...

```

### 5. 分支

```shell
$ git branch                        # 列出所有本地分支
$ git branch -r                     # 列出所有远程分支
$ git branch -a                     # 列出所有本地分支和远程分支
$ git branch [branch-name]          # 新建一个分支，但依然停留在当前分支
$ git checkout -b [branch]          # 新建一个分支，并切换到该分支
$ git checkout [branch-name]        # 切换到指定分支，并更新工作区
$ git checkout -                    # 切换到上一个分支
$ git merge [branch]                # 合并指定分支到当前分支
$ git branch -d [branch-name]       # 删除分支
$ git push origin --delete [branch-name]   # 删除远程分支
$ git branch -dr [remote/branch]
$ git branch -v                     #查看当前所在分支的
$ git branch -m [branch-name]       #修改当前分支名
$ git branch push [remote] [branch-name] #将当前分支提交到远程仓库的分支
```

### 6. 标签

```shell
$ git tag        # 列出所有tag
$ git tag [tag-name]  # 新建一个tag在当前commit
$ git tag [tag] [commit]  # 新建一个tag在指定commit
$ git tag -d [tag]  # 删除本地tag
$ git push origin :refs/tags/[tagName] # 删除远程tag
$ git show [tag] # 查看tag信息
$ git push [remote] [tag] # 提交指定tag
$ git push [remote] --tags  # 提交所有tag
$ git checkout -b [branch] [tag] # 新建一个分支，指向某个tag
```

### 7. 查看

```shell
$ git status                           # 显示有变更的文件
$ git log                              # 显示当前分支的版本历史
$ git shortlog -sn                     # 显示所有提交过的用户，按提交次数排序
$ git blame [file]                     # 显示指定文件是什么人在什么时间修改过
$ git diff                             # 显示暂存区和工作区的代码差异
$ git diff --cached [file]             # 显示暂存区和上一个commit的差异
$ git show [commit]                    # 显示某次提交的元数据和内容变化
$ git rebase [branch]                  # 从本地master拉取代码更新当前分支：branch 一般为master
```

### 8. 远程同步

```shell
$ git remote update                         #更新远程仓储
$ git fetch [remote]                        # 下载远程仓库的所有变动
$ git remote -v                             # 显示所有远程仓库
$ git remote show [remote]                  # 显示某个远程仓库的信息
$ git remote add [shortname] [url]          # 增加一个新的远程仓库，并命名
$ git pull [remote] [branch]                # 取回远程仓库的变化，并与本地分支合并
$ git push [remote] [branch]                # 上传本地指定分支到远程仓库
$ git push [remote] --force                 # 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --all                   # 推送所有分支到远程仓库
```

### 9.  撤销

```shell
$ git checkout [file]                       # 恢复暂存区的指定文件到工作区
$ git checkout [commit] [file]              # 恢复某个commit的指定文件到暂存区和工作区
$ git checkout .                            # 恢复暂存区的所有文件到工作区
$ git reset [file]                 # 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset --hard                 # 重置暂存区与工作区，与上一次commit保持一致
# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]
# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]
# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]
```

