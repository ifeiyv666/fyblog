---
title: Git命令
categories:
  - Git
tags:
  - Git
date: 2020-06-13 17:30:07
---



### Git命令

安装Git就不在这里记录了，只记录使用。并且是在MAC环境下，Window环境可能会有少许的差异。

#### 一 、初始化一个本地化仓库

1. 首先选择一个要存储的目录,创建一个要管理的 `GitStudy`目录

   ```shell
   mkdir GitStudy
   ```

2. 进入到`GitStudy`目录

   ```shell
   cd  GitStudy
   ```

3. 使用`git init`初始化仓库,会在 `GitStudy`目录下创建一个 `.git` 的隐藏文件夹

   ```shell
   git init
   ```

   

#### 二、版本控制

1. `git add <file>` 把改动或新建的文件添加到暂存区

   ```shell
   git add readme.txt
   ```

2. `git commit -m <message>` 确认把暂存区的文件提交到当前的分支

   ```shell
   git commit -m "add readme.txt"
   ```

   提交后输出信息

   ```verilog
   [master (root-commit) 80af25d] add readme.txt
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 readme.txt
   ```

   

3. 版本回退

   - git log 查看历史记录
   - git log --pretty=oneline (只会输出版本号和提交的message日志)

   ```shell
   git reset #回退上一个版本
   
   git reset --hard HEAD^  #回退上一个版本
   
   git reset --hard <版本号> #回退到版本号对应的版本，回退之后，也可以通过这个命令返回回退之前的版本
   ```

   - 如果记不住版本号可以用 `git reflog`命令查看记录,最前面的字符串就是<版本号>

     ```verilog
     143e5ea (HEAD -> master) HEAD@{0}: commit: add code1.txt
     80af25d HEAD@{1}: commit (initial): add readme.txt
     ```

4. 丢弃工作区的修改：

   ```shell
   git checkout -- readme.txt
   
   # 如果没有git add 加入缓存区，此文件所有更改被撤销
   # 如果已经被 git add 或者 git commit 回退没有效果
   # 如果 git add 或者 git commit 之后进行修改了，回退到 git add 或者 git commit 之后的状态
   ```

   

####  三、添加远程库

1. 在本地的 `GitStudy`  （根据实际情况，我上面创建的是GitStudy目录）目录下面运行命令：

   ```shell
   git remote add origin https://gitee.com/用户名/GitStudy.git
   ```

2. 把本地库推送到远程分支

   ```shell
   git push -u origin master
   ```

   

#### 四、从远程库克隆

```shell
git clone -b master https://gitee.com/用户名/GitStudy.git
```



#### 五、创建与合并分支

1. 创建dev分支，切换到dev

   ```shell
   git checkout -b dev
   
   #log  
   #Switched to a new branch 'dev'
   
   # -b 表示创建并且进行切换,相当于执行了以下两个命令
   # git branch dev （创建dev分支）
   # git checkout dev （切换到 dev分支）
   ```

   或者 新版本加入了 `switch` 切换分支命令

   ```shell
   git switch -c dev #创建并切换到新的dev分支
   
   git switch dev #直接切换到已有的dev分支
   ```

   

2. 查看当前分支

   ```shell
   git branch
   
   #log
   # *dev
   # master
   
   # 前面带*，表示当前所在的分支
   ```

   

3. 合并分支,假设要把dev分支合并到master分支

   ```shell
   #如果当前在dev分支,首先要切换到master分支，如果当前是在master分支，则不需要切换分支
   
   git checkout master #当前已经切换到master分支
   
   #执行合并命令
   
   git merge dev
   
   ```

4. 删除分支

   ```shell
   # 如果上面dev分支不需要了，可以保留，也可以进行删除
   # ****删除的时候当前分支不要是处于被删除的分支***
   
   git branch -d dev
   
   # log
   # Deleted branch dev (was f23g67u).
   
   
   # 如果检出一个分支用来开发新分支，进行开发。
   # 在后来不进行合并，直接删除，会提示分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用大写的-D参数
   git branch -D test  #强制删除 test 分支
   
   ```

5. 解决冲突

   ```shell
   #找到冲突文件,打开
   
   # Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容的冲突部分
   
   # 根据情况删除掉不要的， git add <filename> 暂存 ，commit提交 
   ```

6. Bug分支

   ```shell
   #使用场景
   
   # 当前dev分支任务未完成，不能提交。而在另外一个test分支又需要进行修改。
   # 这个时候需要把现在的工作现场 存储 起来，等以后继续操作。
   git stash #暂存当前工作现场
   
   #这个时候就可以切换到其他分支，做其他工作了
   git checkout test
   
   #如果test分支工作完成了，并且已经提交。要切换回我们的dev分支，继续进行未完的工作。
   git checkout dev
   
   #接下来就要恢复现场，有两种方式
   
   # 查看
   git stash list #可以查看所有的已经存储的现场
   
   # 第一种方式
   git stash apply #恢复现场 但是stash存储的内容并不删除
   git stash drop  #删除stash存储的数据
   
   # 第二种方式
   git stash pop #恢复现场，并且删除stash存储的数据
   
   
   ```

   

#### 六、tag标签

1. 创建tag标签

   ```shell
   git tag v1.0
   ```

2. 查看tag标签

   ```shell
   git tag
   
   #log
   # v1.0
   ```

3. 操作标签

   ```shell
   git tag -d v1.0 #删除标签（删除本地标签）
   
   git push origin v1.0 #推送tag标签到远程
   
   git push origin --tags #推送全部尚未推送到远程的本地标签
   
   #如果要删除推送到远程的tag标签需要两步：
   # 1.先删除本地的标签
   git tag -d v1.0
   # 2.删除远程的tag标签
   git push origin :refs/tags/v1.0
   ```

   

