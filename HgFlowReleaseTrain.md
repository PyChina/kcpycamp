[Hg](HgUsage.md),[協同模型](HgFlows.md)
:[无政府](HgFlowAnarchy.md)
|[单一中央](HgFlowCentralAlone.md)
|[托管中央](HgFlowCentreDepository.md)
|[分支仓库](HgFlowBranchRepos.md)
|[特性分支](HgFlowBranchFeatures.md)
|[发布列车](HgFlowReleaseTrain.md)
|[内核模型](HgFlowLiunxKernel.md)
|[写共享](HgFlowShaReadWrite.md)

# Hg工作流:发布列车 #


参考: **[Mercurial 权威指南 第 5 章 团体协作](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/collaborating-with-other-people.html)**


## 概述 ##
和[特性分支](HgFlowBranchFeatures.md) 基本相同,关键的差异是:
  1. 团队作品的版本每次只维护一个版本
  1. 旧版本关闭在历史分支中不在打开

> 策略图谱如下::
```

O-->O-->[]                                          仓库初始主线
         \
          +-->O-->O-->O-->[]                        版本车厢1
                           \
                            +-->O-->O-->O--@        当前版本车厢
                            ...
   
图例:
    O   版本
    []  标签
    +   合并
    @   tip
```


## 操作 ##
  * 初始化工程仓库后,大家就可以克隆之,加入开发
```
$ hg init main
$ cd main
$ echo 'This is a boring feature.' > myfile
$ hg commit -A -m 'We have reached an important milestone!'
adding myfile
```
  * 开始分支前,一般要进行标签操作
```
$ hg tag v1.0
#   随时可以查阅标签状态
$ hg tags
tip                                1:dc6fc637529e
v1.0                               0:2a88e5028cd9
```
  * 团队统一跃迁入一个新版本开发时,组长启动
```
$ hg branch release_v1.1
標記工作目錄為release_v1.1分支

$ hg branches
release_v1.1                       34:7e3729edd125
default                            33:dc6fc637529e
$ hg push
正在推到 https://bitbucket.org/ZoomQuiet/pycamp.lanim
正在搜索修改
中止: push 建立新的遠端分支 'TryTkGUI'!
(使用 'hg push --new-branch' 建立新的遠端分支)

$ hg push --new-branch
正在推到 https://bitbucket.org/ZoomQuiet/pycamp.lanim
正在搜索修改
遠端: adding changesets
遠端: adding manifests
遠端: adding file changes
遠端: added 2 changesets with 1 changes to 1 files
```
  * 团队成员统一更新到对应分支后,进行正常的 [托管中央](HgFlowCentreDepository.md) 式協作
```
$ echo 'This is exciting and new!' >> myfile
$ hg commit -m 'Add a new feature'
$ hg up default
1個更新 0個合併 0個移除 0個未解決

$ hg push
正在推到 https://bitbucket.org/ZoomQuiet/pycamp.lanim
正在搜索修改
遠端: adding changesets
遠端: adding manifests
遠端: adding file changes
遠端: added 2 changesets with 1 changes to 1 files
```

## 蟒营建议 ##

**我们就基于这一模型进行!**
  * 因为每一期蟒营持续时间不长
  * 但是要求至少使用周迭代节奏
  * 每周将前周开发关闭,启动新分支,进行迭代




---


