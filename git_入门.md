# Git 入门

### 推荐教程
> [Git 教程 - 廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

### 重要概念
* 集成式vs分布式
* 工作区、暂存区和版本库

### 基本命令
* 工作区 --> 暂存区*（需要注意tracked和untracted的区别）*
	* **git add <file&gt;**
    * **git add -A**  stages All
    * **git add .**   stages new and modified, without deleted
    * **git add -u**  stages modified and deleted, without new                    
* 暂存区 --> 版本库
	* git commit -m "comments"	提交暂存区的内容
* 工作区撤销操作
	* **git checkout -- <file&gt;** 撤销文件改动
* 暂存区撤销操作
	* **git reset HEAD <file&gt;** 将暂存区撤销到上一步，即回到工作区
	* 再执行一次工作区撤销操作
* 版本库撤销操作
	
* 暂存区撤销操作
	* **git rm --cached <file&gt;** 撤销文件添加(文件夹需再加 -r)