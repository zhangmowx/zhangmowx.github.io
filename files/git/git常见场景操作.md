## Git常见场景操作

### 1. 本地项目如何提交到远程仓库

例如本地有个crm项目，需要提交到github中（项目无版本管理）

- 在crm项目根目录下，使用`git init`进行初始化仓库

  ```shell
  $ git init
  Initialized empty Git repository in E:/git-demo/crm/.git/
  ```

- 在github中创建新的repository。github中名称可以和本地项目名不同

  https://github.com/zhangmowx/mycrm.git

  ![](..//images/git/github创建repository.png)

- 本地代码提交到本地仓库

  ```shell
  git add *                         #将代码添加到暂存区
  git commit -m "frist commit"      #将代码提交到本地库
  ```

- 在本地仓库创建一个远程仓库地址

  ```shell
  #本地仓库关联远程仓库，并给远程仓库命名为github-crm
  $ git remote add github-crm https://github.com/zhangmowx/mycrm.git
  #查看所有远程仓库地址
  $ git remote -v
  github-crm      https://github.com/zhangmowx/mycrm.git (fetch)
  github-crm      https://github.com/zhangmowx/mycrm.git (push)
  ```

- 将本地仓库代码提交到远程仓库

  ```shell
  #将本地代码提交到github中，git push 远程仓库名 指定远程仓库中的哪个分支
  git push github-crm master
  ```

  

### 2. 多人分支开发时，提交到远程仓库出现冲突

当本地开发的代码提交到本地仓库后，提交到远程仓库报错。发生代码冲突。

```shell
$ git push github-crm dev_20200418
To https://github.com/zhangmowx/mycrm.git
 ! [rejected]        dev_20200418 -> dev_20200418 (fetch first)
error: failed to push some refs to 'https://github.com/zhangmowx/mycrm.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

- 使用git pull将远程代码更新到本地仓库

  ```shell
  # git pull [remote] [branch-name] 将远程代码更新到本地仓库
  $ git pull github-crm dev_20200418
  remote: Enumerating objects: 15, done.
  remote: Counting objects: 100% (15/15), done.
  remote: Compressing objects: 100% (11/11), done.
  remote: Total 12 (delta 1), reused 0 (delta 0), pack-reused 0
  Unpacking objects: 100% (12/12), done.
  From https://github.com/zhangmowx/mycrm
   * branch            dev_20200418 -> FETCH_HEAD
     0786fc1..bcfd518  dev_20200418 -> github-crm/dev_20200418
  Auto-merging java/1.txt    
  CONFLICT (content): Merge conflict in java/1.txt   # CONFLICT 出现冲突，列出冲突文件名
  Automatic merge failed; fix conflicts and then commit the result
  ```

  ![](..//images/git/提交时冲突显示.png)

- 打开冲突文件,进行修改

  ```shell
  <<<<<<< HEAD   #HEAD表示远程仓库中的代码
  
  zhangmo新增了x功能，2020xxxx
  zhangmo新增了y功能，2020xxxx
  zhangmo新增了Z功能，2020xxxx
  =======               #这部分表示本地仓库的代码
  新增了a功能，2020xxxx
  新增了b功能，2020xxxx
  新增了c功能，2020xxxx
  >>>>>>> bcfd51875db6178a8cc170c233fa16d7d49c1dec
  
  #对文件进行修改
  zhangmo新增了x功能，2020xxxx
  zhangmo新增了y功能，2020xxxx
  zhangmo新增了Z功能，2020xxxx
  
  新增了a功能，2020xxxx
  新增了b功能，2020xxxx
  新增了c功能，2020xxxx
  ```

- 重新进行`git add`、`git commit`操作。因为pull的代码可能还有本地仓库没有（参考上图3.txt文件）

- 重新push代码，提交成功

  ```shell
  $ git push github-crm dev_20200418
  Enumerating objects: 15, done.
  Counting objects: 100% (15/15), done.
  Delta compression using up to 8 threads
  Compressing objects: 100% (8/8), done.
  Writing objects: 100% (9/9), 864 bytes | 432.00 KiB/s, done.
  Total 9 (delta 1), reused 0 (delta 0)
  remote: Resolving deltas: 100% (1/1), done.
  To https://github.com/zhangmowx/mycrm.git
     bcfd518..8274b5b  dev_20200418 -> dev_20200418
  
  ```

  

### 3. 分支代码合并到master时，发生冲突。

例如有远程分支dev_20200418，需要合并到远程master

- 在远程master和dev_20200418都pull到本地。

- 切换到本地master中

  ```shell
  $ git checkout master
  Switched to branch 'master'
  ```

- 将本地的dev_20200418分支合并到本地master中。可能会发生代码冲突

  ```shell
  $ git merge dev_20200418
  Auto-merging java/1.txt
  CONFLICT (content): Merge conflict in java/1.txt  # 1.txt发生冲突
  Automatic merge failed; fix conflicts and then commit the result. 
  ```

- 打开冲突文件进行修改

- 重新进行`git add`、`git commit`操作

- 重新push到远程master

  ```shell
  git push github-crm master
  ```

  