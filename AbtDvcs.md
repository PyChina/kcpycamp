**PythoniCamp**::[目标](GoalPythoniCamp.md)![参与](HowtoJoin.md);[流程](KcPyCampFlow.md);[作品](PythoniCampItems.md):[开发](HowtoDevelop.md);[资源](PythonicRes.md);[讨论](HowtoDiscuss.md);[SCM](HowtoScm.md);[测试](HowtoTesting.md)...

# DVCS #
~ **D\*istributed**V\*ersion **C\*ontrol**S\*ystem


## 概述 ##
有别于主流的CVS/SVN 等版本仓库软件, Hg 是种新兴的[分布式版本控制系统(DVCS)](http://wiki.woodpecker.org.cn/moin/DistributedScm),简单的说:
  1. 所有开发成员是平等的共同拥有所有代码的一切变化
  1. 代码的变更首先保存在本地仓库,然后根据情况`推`或是`拉`到其它仓库

### 给SVN用户的1分钟解说 ###
其实分布式的名称,策略神马的不重要的,重要的是团队配合!
  * 基于版本仓库的配合,原则从来没有变过,不论什么系统:
    1. 每个人都对团队代码负有职责!
    1. 在发布你的修订前,有责任确信没有引发冲突
    1. 在不清楚他人的相关修订前,不能轻易的否决别人的修订,强行合并
Hg 不过,是给大家更加的自由,在没有网络的情况下,依然可以进行安全的版本记录
是的,大家完全可以将 Hg 当成 SVN 来用,唯二注意的是:
    1. `hg up` 只是更新本地仓库和工作复本的差异,要从团队仓库更新是下拉 `hg pull`
    1. `hg ci` 只是检入到本地仓库,要将修订发布给所有人是上推 `hg push`

`其它的,和SVN 的操作完全类似`


## 5分钟说明主要观念 ##

**核心概念**:
  * 集中式版本控制聚焦于**同步**(synchronizing),**追溯**(tracking), 和**备份**(backing up)档案.
    * ![http://kcpycamp.googlecode.com/files/centralized_example.png](http://kcpycamp.googlecode.com/files/centralized_example.png)
  * 分布式版本控制聚焦于 **分享变更** (sharing changes) ; 每个\*变更集**具有**全域唯一辨识码**(guid-global unique id)或unique id .
    * ![http://kcpycamp.googlecode.com/files/distributed_example.png](http://kcpycamp.googlecode.com/files/distributed_example.png)
  ***记录**(Recording)/**下载**(Downloading) 以及采用(applying) 一个\*变更集**被视为是不同的步骤 (在集中式系统, 此三者同时发生).
  * 分布式系统没有强制的架构. 你可以建立"中央管理"区或让个人保持各自端运作.

**术语**:
  * **推(push)**: 将变更送给其它的**仓库**(repository) (应该需要其它repository拥有者的允许)
  * **拉(pull)**: 从另一**仓库**(repository)抓资料

**关键优势:**
  * 每人都有其 **本地沙盒**(local sandbox). 你可以在自己的工作空间中修改或恢复旧版, 不需要大量的**检入**(checkins). 你自己的工作记录都累积存在自己的 **仓库**repository.
  * **可离线工作**. 只有当你想分享修订时才需要上线. 否则可一直在自己的工作机上独立作业/签入(check in)/复原(undo), 没有所谓"服务器"当掉或在飞机上的问题.
  * 速度很快. **差异**(diff), **提交**(commit)与**恢复**(revert)都在本端即可完成. 没有因网络或服务器不稳而必须用一年前开发版本的问题.
  * 可妥善做变动的处理. DVCS针对分享的变更做建置. 每个变更都有其独一无二的辨识码(guids)以方便追踪.
  * **分支**(Branching)与**合并**(merging)很容易. 因为每一开发人员"有自己的分支", 每一分享的变动就像交换整合. 但guids让自动组合变更与避免重复动作简单容易.
  * 较少的管理. DVCS很容易执行; 没有所谓的“总在运作的”服务器软件需要安装. 此外, DVCS也不太需要你去"加"新的使用者; 你只需选择想从那里**拉(pull)**资料的URLs. 这样可以避免大型项目中令人头痛的政治性问题.


**心理劣势**
  * 仍需要备份. 用DVCS, 你仍希望可以有台机器让你push所有的变更到他那里保存“以防万一”. (在Subversion, 你有一台随时待命的机器做主要的数据贮存库, 建议您在DVCS也做一样的事).<sup>code.google 以及bitbucket.org/github.com 等等,有很多免费的公开DVCS空间</sup>
  * 没有所谓的`最近的版本` 存在. 如果没有集中地, 你无法马上知道要到谁那儿的仓库取得最近变更的 **版本**(version). 再者, 一个中央集中地才可帮助大家清晰知道最近的"稳定版本"为何.
    * ~ 不过,这完全的团队内部约定的事儿,和集中式仓库不同,不依赖工具强行管理;
    * 而是更加民主和人为的进行 **版本**(version)的识别/评定/发布
  * 没有真正的 **修订版号**(revision numbers). 每一贮存库有依变更做出的修订版号码. 和传统的贮存库不同的方法,人们依变更的修订号码做沟通: "请问你有变更号码 fa33e7b? " (记住, 这ID是一个不好看的guid总体唯一辨识码). 还好, 你可以用有意义的名字贴标你发布的版本.



### 核心名词 ###
| **概念** | **翻译** | **説明** | **备注** |
|:-----------|:-----------|:-----------|:-----------|
| REPOSITORY | 仓库 | Hg 保存修订的空间 | 一般在 .hg 隐藏目录中 |
| WORKING DIR | 工作目录 | 我们进行开发的地方 | 普遍的目录 |
| CHANGESET | 变更集 | 某次提交的改变集合 | **即:**不论一次修订了几行/几个文件,作为提交,都自动集成算一次 <sup>简称: cset</sup> |
| **概念** | **翻译** | **説明** | **备注** |
| REV | 修订版号 | 标识某次变更的号码 | 正整数 |
| REVISION | 修订版 | 合并到仓库中的改变集 |  |
| PARENT | 父版本 | 在工作目录中某修订版的直属祖辈 |  |
| BRANCH | 分支 | 跟从某修订版的指定子版本系列 |  |
| MEARGE | 合并 | 有两个父版本的修订版 | **即:** 将同一文件的多个版本合并成新的一个版本 |
| HEAD | 头部 | 某分支最新的修订版 | 类似数据库的游标,永远指向分支的最后一个版本 |
| TIP | 顶部 | 最新的头部 | 在一个仓库中可以存在多个分支,每个分支都有 HEAD,但是整个仓库整体来看只有一个 TIP |
| **概念** | **翻译** | **説明** | **备注** |
| PATCH | 补丁 | 文件从版本1<sup>简记:R1</sup>更新到版本2需要的数据 | **即:** 版本间的差异,可以涉及多个文件的变化|
| BYNDLE | 打包 | 支持文件许可和重命名的补丁  | **即:** 以文件形式进行传播的补丁 |
| **概念** | **翻译** | **説明** | **备注** |


## 参考 ##
**[DVCS(Distributed Version Control System)說明](http://blog.csdn.net/esebella/archive/2009/07/04/4321239.aspx)**
  * [分布式配置管理](http://wiki.woodpecker.org.cn/moin/DistributedScm)<sup> - Woodpecker Wiki for CPUG</sup>




---

TOC: 