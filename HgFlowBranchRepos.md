[Hg](HgUsage.md),[協同模型](HgFlows.md)
:[无政府](HgFlowAnarchy.md)
|[单一中央](HgFlowCentralAlone.md)
|[托管中央](HgFlowCentreDepository.md)
|[分支仓库](HgFlowBranchRepos.md)
|[特性分支](HgFlowBranchFeatures.md)
|[发布列车](HgFlowReleaseTrain.md)
|[内核模型](HgFlowLiunxKernel.md)
|[写共享](HgFlowShaReadWrite.md)

# Hg工作流:使用多个分支仓库工作 #


参考: **[Mercurial 权威指南 第 5 章 团体协作](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/collaborating-with-other-people.html)**


## 概述 ##
Hg 本身支持灵活的仓库合并策略,所以,多分支仓库的协同策略,其实就是:
  1. 根据工程的不同阶段,克隆成不同的分支仓库
  1. 多个分支在不同的仓库并行开发
  1. 人工判定何时合并

> 策略图谱如下::
```
O----------[]--->O--->O---@     B2      版本2仓库
          /      |
O------->O--+>O--+O-------@     main    主仓库
  \         |
O--[]-->O-->O-------------@     B1      版本1仓库

图例:
    O   版本
    []  标签
    +   合并
    @   tip
```

> 常见的情景是::
    * 作品的各个发布版本,在分支点处打好发布标签后,独立克隆成分支仓库,并由专人长期维护
    * 作品的版本分支仓库,一般只解决问题,不引入新特性
      * 每当完成针对性的增补后,合并回主仓库
    * 主仓库作为未来版本的开发线
      * 不时的接受版本分支仓库的重要改进,吸收为下一版本的特性

## 操作 ##
```
$ hg init main
$ cd main
$ echo 'This is a boring feature.' > myfile
$ hg commit -A -m 'We have reached an important milestone!'
adding myfile
#   初始化工程仓库后,大家就可以克隆之,加入开发
#   开始分支前,一般要进行标签操作
$ hg tag v1.0
$ hg tip
changeset:   1:dc6fc637529e
tag:         tip
user:        Bryan O'Sullivan <bos@serpentine.com>
date:        Thu May 21 09:13:33 2009 +0000
summary:     Added tag v1.0 for changeset 2a88e5028cd9

#   随时可以查阅标签状态
$ hg tags
tip                                1:dc6fc637529e
v1.0                               0:2a88e5028cd9

#   假设,另外的成员,进行特性开发时...
$ cd ../main
$ echo 'This is exciting and new!' >> myfile
$ hg commit -m 'Add a new feature'
$ cat myfile
This is a boring feature.
This is exciting and new!

#   克隆成对应专用仓库
$ cd ..
$ hg clone -rv1.0 main stable
requesting all changes
adding changesets
adding manifests
adding file changes
added 1 changesets with 1 changes to 1 files
updating working directory
1 files updated, 0 files merged, 0 files removed, 0 files unresolved

#   进行版本修订时,也可以继续克隆出对应仓库的 hotfix 仓库
$ hg clone stable stable-fix
updating working directory
1 files updated, 0 files merged, 0 files removed, 0 files unresolved
$ cd stable-fix
$ echo 'This is a fix to a boring feature.' > myfile
$ hg commit -m 'Fix a bug'
$ hg push
pushing to /tmp/branching7dH5UD/stable
searching for changes
adding changesets
adding manifests
adding file changes
added 1 changesets with 1 changes to 1 files

#   进行合并时,要日常明确合并的方向和仓库名
$ cd ../main
$ hg pull ../stable
pulling from ../stable
searching for changes
adding changesets
adding manifests
adding file changes
added 1 changesets with 1 changes to 1 files (+1 heads)
(run 'hg heads' to see heads, 'hg merge' to merge)
$ hg merge
merging myfile
0 files updated, 1 files merged, 0 files removed, 0 files unresolved
(branch merge, don't forget to commit)
$ hg commit -m 'Bring in bugfix from stable branch'
$ cat myfile
This is a fix to a boring feature.
This is exciting and new!

```
## 蟒营建议 ##
  * 如果熟练的掌握了在本地局域网进行多仓库合并的操作,那么可以这么用
  * 但是,一般情况下,很难避免团队成员误解了仓库名的含义,进行了错误的合并

**所以,不建议进行这种协同!**


---


