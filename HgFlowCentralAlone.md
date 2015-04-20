[Hg](HgUsage.md),[協同模型](HgFlows.md)
:[无政府](HgFlowAnarchy.md)
|[单一中央](HgFlowCentralAlone.md)
|[托管中央](HgFlowCentreDepository.md)
|[分支仓库](HgFlowBranchRepos.md)
|[特性分支](HgFlowBranchFeatures.md)
|[发布列车](HgFlowReleaseTrain.md)
|[内核模型](HgFlowLiunxKernel.md)
|[写共享](HgFlowShaReadWrite.md)

# Hg工作流:单一中央仓库 #


参考: **[Mercurial 权威指南 第 5 章 团体协作](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/collaborating-with-other-people.html)**


## 概述 ##
这就是以往大家熟知的集中式版本管理系统的统一模型:
  1. 设定一个本地中央版本仓库
  1. 每个进入团队的人,首先克隆出中央仓库
  1. 定期同步中央仓库,解决冲突,上推中央仓库

> 策略图谱如下::
```

  |---->O--+O--->O----@     张三成员版本库
 /        / |
O-----+O-/--+>O--+O---      Central    中央仓库
 \    |        \ |
  |-->O-->O-----+O----      李四成员版本库
   ...
   
图例:
    O   版本
    []  标签
    +   合并
    @   tip
```

> 常见的情景是::
    * 刚刚从 CVS/SVN/VSS 集中式版本管理模型中迁移过来的团队,大家不论从心理而是知识方面都没有过渡到分布式協同
    * 所以,将 Hg 用成了  CVS/SVN/VSS
      * 依然要每日同步团队所有变更
      * 依然要尝试解决人为的冲突
      * 依然要抢先上推中央仓库,以免背负冲突的解决职责


## 操作 ##
```
$ hg clone http://192.168.*.*:*** locREPO
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
pulling from http://192.168.*.*:***
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
  * 团队,进入 Hg 仓库初期,可进行一段时期的这种協作
  * 理解了分布式仓库之后,就应该根据团队的开发节奏:
    1. 根据任务,事先划分好模块/目录/文件
    1. 进行各个任务承担人的本地快速实验式开发
    1. 在每日约定的固定时间,逐一合并成员修订,集体解决冲突,收获日稳定版本标签


---


