# Git start

学习地址：http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

一、重要概念
    1. 集成式vs分布式
	2. 工作区、暂存区和版本库
	3.

二、基本命令
    1. 工作区 --> 暂存区
        注：需要注意tracked和untracted的区别

        git add <file>
        git add -A  stages All
        git add .   stages new and modified, without deleted
        git add -u  stages modified and deleted, without new

        逆向操作：（撤销添加）
        git checkout -- <file>      撤销文件改动(只能撤销tracted的文件，不能撤销untracted的文件(即新添加的文件))
        git rm --cached <file>      撤销文件添加(文件夹需再加 -r)