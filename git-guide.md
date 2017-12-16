# git 规范

## 简介

该文档主要的设计目标是提高使用git协作的团队一致性与可维护性。

## 使用 git-flow 进行有效的分支实践

git-flow 是一个 git 扩展集，按 Vincent Driessen 的分支模型提供高层次的库操作。

### 指南
http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html

1. 初始化 git flow init
   必须回答几个问题，使用默认值即可。

2. 增加新特性 git flow feature start MYFEATURE-MYNAME
   新特性的开发基于'develop'分支，并切换到这个分支下

3. 完成新特性 git flow feature finish MYFEATURE-MYNAME
   合并特性分支到'develop'，并删除新特性分支切换到'develop'分支。

4. 合作开发新特性时。
   (1)git flow feature pull origin MYFEATURE取得一个发布的新特性分支，并签出远程的变更，也可以使用git flow feature track MYFEATURE
   (2)git flow feature pulish MYFEATURE 发布新特性到远处服务器

## 提交分支commit

git add --all
git status  查看变动文件
git commit --verbose 列出diff结果

提交commit时，必须给出完整的扼要的提交信息，列出改动的点及原因

## 与主干同步

分支开发过程中与主干要经常 保持同步

git fetch origin
git rebase origin/master

## 合并commit

###方案一

用与处理多个commit合并
git rebase -i origin/master

pcick 正常选中
reword 选中，并且修改提交信息
edit 选中，rebase时会暂停，允许你修改这个commit
squash 选中， 会将当前commit与上一个commit合并
fixup 与squash相同， 但不会保存当前commit的提交信息
exec 执行其他shell命令

###方案二

先撤销过去5个commit，建立一个新的

git reset HEAD~5
git add .
git commit -am "Here's the bug fix that close"
git push --force

squash和fixup命令，可以当命令行参数使用，自动合并commit

git commit --fixup
git rebase -i --autosquash

## 推送到远程仓库

git push --force origin myfeature

## 发出Pull Request

提交到远程仓库后，就可以发布Pull Request到master分支，请求review合并到develop分支

## 具体可参考http://www.ruanyifeng.com/blog/2015/08/git-use-process.html
