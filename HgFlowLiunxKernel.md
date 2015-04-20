[Hg](HgUsage.md),[協同模型](HgFlows.md)
:[无政府](HgFlowAnarchy.md)
|[单一中央](HgFlowCentralAlone.md)
|[托管中央](HgFlowCentreDepository.md)
|[分支仓库](HgFlowBranchRepos.md)
|[特性分支](HgFlowBranchFeatures.md)
|[发布列车](HgFlowReleaseTrain.md)
|[内核模型](HgFlowLiunxKernel.md)
|[写共享](HgFlowShaReadWrite.md)

# Hg工作流:Linux 内核模型 #


参考: **[Mercurial 权威指南 第 5 章 团体协作](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/collaborating-with-other-people.html)**


## 概述 ##
这是纯正的 [DVCS](AbtDvcs.md) 模型協作, Linux 创始人 Linus 更是针对这一模型,专门写了 Git 版本管理系统!

简单的说,就是 `分层次` 的 **拉-合并** :
  1. 每个人都从自己领域的主持人那克隆仓库
  1. 完成修订后,通知主持人可以下拉什么特性
  1. 主持决定是否下拉/合并
  1. 主持人进一步定期,向核心主持人通知下拉

> 策略图谱如下::
```

  O--->O-------O--^O--@    Kernel 仓库
   \              |
    |             |
    |    ->O->O   |        组件贡献者仓库
    |   /     |   |
    `->O------VO-^O--->    组件主持人仓库
       \         |
        `->O->O->O         组件贡献者仓库

图例:
    O   版本
    +   上推合并
    ^V  下拉合并
    []  标签
    @   tip
```

> 常见的情景是::
    * 一个复杂的系统,根据架构,分成了有针对性的组件
    * 每个组件维护团队,形成 各自的类似 [分支仓库](HgFlowBranchRepos.md)协作模型
      * 只是和 [分支仓库](HgFlowBranchRepos.md) 不同的在于: `任何人都没有权力直接写他人的仓库!`
    * 组件团队成员到组件团队仓库,以及 组件团队仓库 到核心仓库 的代码合并,都通过人工下拉的形式完成

## 操作技巧 ##
作为主持人,需要管理多个仓库的修订合并事务,就需要进行仓库的聲明:
  * 在本地仓库的 `.hg/hgrc` 中增补:
```
[paths]
default = https://bitbucket.org/alice/[project]
bob = https://bitbucket.org/bob/[project]
tom = https://bitbucket.org/tom/[project]
...
```
  * 这样就可以针对成员仓库的别名进行快速查阅,决定是否进行 `下拉-合并`
```
$ hg in bob
正在跟 https://bitbucket.org/bob/[project] 比對
正在搜索修改
没有发现修改

$ hg in tom
正在跟 https://bitbucket.org/bob/[project] 比對
正在搜索修改
修改集:      248:08940bcc62d9
标签:        tip
用户:        Zoom.Quiet
日期:        Thu Mar 31 14:26:49 2011 +0000
摘要:        Edited wiki page HgFlowAnarchy through web user interface.

$ hg diff tom
diff -r 8ba58e5a7fdc HgFlowAnarchy.wiki
--- a/HgFlowAnarchy.wiki	Thu Mar 31 20:50:32 2011 +0800
+++ b/HgFlowAnarchy.wiki	Thu Mar 31 22:28:27 2011 +0800
@@ -1,4 +1,4 @@
-#summary Hg工作流:特性分支
+#summary Hg工作流:无政府
 #labels Hg,WorkFlow,Howto,SCM
 
 [HgUsage Hg],[HgFlows 協同模型]

$ hg pull -u
$ hg ci -m "接受成员修订"
$ hg push
```


> 参考::
    * [INET6: [Mercurial](http://floss.zoomquiet.org/data/20101106092609/index.html)多來源更新]

## 蟒营建议 ##
原[蟒营協作](HgFlowOldCamp.md) 是这么设计的
  * [作品团队组长管理规约](HgTeaMana.md)
  * [蟒营导师仓库管理规约](HgCampMana.md)

但是,考虑到学习成本太高,而且对于组长的要求太复杂,就放弃了...



---


