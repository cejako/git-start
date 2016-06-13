# Git 入门

### 推荐入门教程
> [Git 教程 - 廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

### 重要概念
* 集成式vs分布式
* 工作区、暂存区和版本库
* 分支
* 标签

### 基本命令
* 创建仓库
	* `git init` 本地新建一个空的仓库
	* `git clone git@github.com:cejako/git-start.git` 从远程库克隆
* 工作区 --> 暂存区*（需要注意tracked和untracted的区别）*
	* `git add <file&gt;`
    * `git add -A`  stages All
    * `git add .`   stages new and modified, without deleted
    * `git add -u`  stages modified and deleted, without new                    
* 暂存区 --> 版本库
	* `git commit -m "comments"`	提交暂存区的内容
* 版本库 --> 远程仓库
	* `git remote add origin git@github.com:cejako/git-start.git` 关联远程仓库
	* `git push origin master` 推送最新修改
* 仓库同步
	* `git fetch origin <branch&gt;` 从远程仓库拉去最新代码，**只拉取代码，不进行合并**
	* `git pull origin <branch&gt;` 相当于git fetch之后git merge，**并跟本地代码进行合并**
	* `git push origin <branch&gt;` 指定分支推送代码至远程仓库
* 工作区撤销操作
	* `git checkout -- <file&gt;` 撤销文件改动
* 暂存区撤销操作
	* `git reset HEAD <file&gt;` 将暂存区撤销到上一步，即回到工作区
	* 再执行一次工作区撤销操作
* 版本库撤销操作
	* `git reset --hard HEAD^` 即版本回退
* 文件删除操作
	* `git rm --cached <file&gt;` 撤销文件添加(文件夹需再加 -r)
* 暂存工作区内容
	* `git stash` 暂存当前工作现场，恢复到上一个commit状态
	* `git stash pop` 恢复上一次暂存的工作区内容
	* `git stash list` 显示所有的工作区暂存内容
	* `git stash clear` 清除所有的工作区暂存内容
	
### 分支
* 创建分支
	* `git checkout -b dev` 创建并 *切换到* dev分支
	* `git branch dev` 创建dev分支
	* `git checkout dev` 切换到dev分支
* 查看分支
	* `git branch` 查看本地分支
	* `git branch -a` 查看本地和远程分支
* 合并分支
	* `git merge dev` 把dev分支合并到当前分支，会优先采用fast-farward模式
	* `git merge --no-ff -m "comments" dev` 多了*--no-ff:* 普通合并，会创建一个新的commit，所以需要*-m*，分支删除后，不会丢失分支历史
* 删除分支
	* `git branch -d dev` 删除dev分支

### 标签
* 添加标签
	* `git tag <tag&gt;` 打一个新标签
* 查看标签
	* `git tag`
* 删除标签
	* `git tag -d <tag&gt;` 删除标签
* 推送标签到远程仓库
	* `git push origin <tag&gt;` 推送至远程仓库
	* `git push origin --tags` 推送全部尚未推送到远程的本地标签
* 删除远程参考标签
	* 先删除本地标签
	* `git push origin :refs/tags/<tagname&gt;` 推送删除标签
