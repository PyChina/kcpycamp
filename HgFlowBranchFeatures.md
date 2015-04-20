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
Hg 本身支持灵活的分支策略,其操作也非常类似 SVN/CVS ;

多分支工作的协同策略,其实就是:
  1. 根据工程的不同阶段,进行分支
  1. 多个分支并行开发
  1. 人工判定何时合并

> 策略图谱如下::
```
         +O-->O-->O---->    B2          版本2分支
        /     |
  O--->O------+O---+O--@    default     主线
   \               |
    `->O-----+O--->O--->    B1          版本1分支
       \     |
        `->O-+              B1-hotfix   版本2紧急修复分支

图例:
    O   版本
    +   合并
    []  标签
    @   tip
```

> 常见的情景是::
    * 作品的各个发布版本,在分支点处打好发布标签后,独立分支出去,并由专人长期维护
    * 作品的版本分支,如果发现重要/紧急问题,为了不影响当前的正常开发
      * 也经常是复制出临时分支
      * 完成针对性的增补后,合并回对应分支,并关闭 hotfix 分支
    * 主线作为未来版本的开发线
      * 不时的接受版本分支的重要改进,吸收为下一版本的特性

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
```
  * 假设,另外的成员,进行特性开发时...
```
$ hg clone main locDev
requesting all changes
adding changesets
adding manifests
adding file changes
added 1 changesets with 1 changes to 1 files
updating working directory
1 files updated, 0 files merged, 0 files removed, 0 files unresolved
$ cd locDev

#   先查询一下分支状态，一般默认有个 default 的
$ hg branches
default                            1:dc6fc637529e

$ hg branch TryTkGUI
標記工作目錄為TryTkGUI分支

$ hg branches
TryTkGUI                           2:7e3729edd125
default                            1:dc6fc637529e

$ echo 'This is exciting and new!' >> myfile
$ cat myfile
This is a boring feature.
This is exciting and new!
$ hg commit -m 'Add a new feature'
$ hg up default
1個更新 0個合併 0個移除 0個未解決

$ hg branches 
TryTkGUI                      3:b3dd239f99de
default                       1:477b035ef460 (inactive)
```
  * 进行合并时,要指明要进行合并的分支名
```
$ hg merge TryTkGUI
1個更新 0個合併 0個移除 0個未解決
(分支已經合併了,別忘了要commit喔)

#   有分支的仓库进行上推时,会有提示
$ hg push
正在推到 https://bitbucket.org/ZoomQuiet/pycamp.lanim
正在搜索修改
中止: push 建立新的遠端分支 'TryTkGUI'!
(使用 'hg push --new-branch' 建立新的遠端分支)
#   可以使用提示的,将分支也推上主仓库
$ hg push --new-branch
正在推到 https://bitbucket.org/ZoomQuiet/pycamp.lanim
正在搜索修改
遠端: adding changesets
遠端: adding manifests
遠端: adding file changes
遠端: added 2 changesets with 1 changes to 1 files

#   也可以,先关闭分支再推上
hg ci --close-branch TryTkGUI
```

## 蟒营建议 ##
`在 Hg 中开/关/合并 分支成本很低`,所以!
  * 建议多用!
  * 在同一仓库中,每个成员都可以拥有自个儿的分支,进行安全的尝试,同时也确保所有人可以知道你在作什么!
  * 但是!**注意:**
    1. 分支的命名! 最好团队内部先约定好,只能启动什么精典的分支,以及分支的命名规范
    1. Hg 分支会对工作目录进行大换血! <sup>将所有文件和目录替换成对应分支中的</sup>
      * 如果工程很大,或是相关分支和主分支的目录结构差异太大,不要轻易使用分支;的确需要的话,也不要轻易合并完全不同目标的两个分支,以便引发混乱
      * 最好是针对稳定主线的小尝试,进行分支测试开发,成功后,立即合并到主线,并关闭分支!

> 参考::
    * [胖豆豆猫的KB-Mercurial实践设想(3) – 大分支](http://www.codingboy.com/zlog/post/28.html)



---


