[Hg](HgUsage.md),[協同模型](HgFlows.md)
:[无政府](HgFlowAnarchy.md)
|[单一中央](HgFlowCentralAlone.md)
|[托管中央](HgFlowCentreDepository.md)
|[分支仓库](HgFlowBranchRepos.md)
|[特性分支](HgFlowBranchFeatures.md)
|[发布列车](HgFlowReleaseTrain.md)
|[内核模型](HgFlowLiunxKernel.md)
|[写共享](HgFlowShaReadWrite.md)

# Hg工作流:托管中央仓库 #


参考: **[Mercurial 权威指南 第 5 章 团体协作](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/collaborating-with-other-people.html)**


## 概述 ##
和[单一中央](HgFlowCentralAlone.md) 基本相同,关键的差异是:
  1. 团队的中央版本仓库,托管在靠谱的项目空间中
  1. 每个进入团队的人,首先克隆出中央仓库
  1. 定期同步中央仓库,解决冲突,上推中央仓库

> 策略图谱如下::
```

  |---->O--+O--->O----@     张三成员版本库
 /        / |
O-----+O-/--+>O--+O---      远程中央仓库  https://bitbucket.org/***
 \    |        \ |
  |-->O-->O-----+O----      李四成员版本库
   ...
   
图例:
    O   版本
    []  标签
    +   合并
    @   tip
```


## 操作 ##
```
$ hg clone https://bitbucket.org/*** locREPO
requesting all changes
adding changesets
adding manifests
adding file changes
added 1 changesets with 1 changes to 1 files
updating working directory
1 files updated, 0 files merged, 0 files removed, 0 files unresolved

$ cd locREPO
$ echo 'This is a fix to a boring feature.' > myfile
$ hg ci -m 'Fix a bug'

#   完成本地仓库检入后,第一时间进行中央仓库的处置
$ hg pull -u
pulling from https://bitbucket.org/***
searching for changes
adding changesets
adding manifests
adding file changes
added 1 changesets with 1 changes to 1 files (+1 heads)
(run 'hg heads' to see heads, 'hg merge' to merge)

#   如果有冲突就解决
$ hg merge
merging myfile
0 files updated, 1 files merged, 0 files removed, 0 files unresolved
(branch merge, don't forget to commit)
$ hg commit -m 'Bring in bugfix from stable branch'

#   然后上推
$ hg push
pushing to /tmp/branching7dH5UD/stable
searching for changes
adding changesets
adding manifests
adding file changes
added 1 changesets with 1 changes to 1 files
```

## 蟒营建议 ##

**我们就基于这一模型进行!**



---


