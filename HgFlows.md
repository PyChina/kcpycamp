# Hg工作流 #


参考: **[Mercurial 权威指南 第 5 章 团体协作](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/collaborating-with-other-people.html)**

## 蟒营協作 ##
> 原则::
    * 简单
    * 稳定
    * 灵活

> 仓库::
    * 我们选择 [bitbucket.org](https://bitbucket.org/) 作为团队开发仓库!
    * 相比 code.google 提供的 Hg 仓库:
      * 更加稳定
      * 限制更加少
      * 控制更加多

### 初始化 ###
  1. 组团,立项,通过评审后,由导师开辟 bitbucket.org 团队仓库,
    * 一般形如: `https://bitbucket.org/ZoomQuiet/pycamp.***`
  1. 组长通过邮件列表,通报 bitbucket.org 帐号,由导师绑定为 仓库管理员

### 团队进入 ###
  1. 成员全部注册 bitbucket.org ,由组长追加为仓库成员,分配写权限
  1. 所有成员,在本地合适的空白目录中克隆团队开发仓库:
    * `hg clone https://bitbucket.org/ZoomQuiet/pycamp.***`
  1. 在仓库目录中,配置身份: `.hg/hgrc`
```
[ui]
username = You Name <you.mailbox@gmail.com>
[paths]
default = https://帐号名:口令@bitbucket.org/ZoomQuiet/pycamp.***
[hostfingerprints]
bitbucket.org = 81:2b:08:90:dc:d3:71:ee:e0:7c:b4:75:ce:9b:6c:48:94:56:a1:fe
```

开始日常开发,協同!

> 建议::
    1. 每天至少检入本地一次修订版本
      * `hg ci -m "修订日志"`
    1. 每周必须同步一次团队仓库,解决冲突,学习团队代码!
      * 先同步:`hg pull -u`
      * 根据提示,进行可能的 `hg heads` 头部查阅; `hg merge tip` <sup>代码合并</sup>
      * 确信没有冲突后,推送到团队远程中央仓库:
```
hg ci -m "检入日志"
hg push
```

### 闭营发布 ###

  1. 完成公开演示和问询
  1. 团队最后一次检查和增补文档,并追加正式发布版本 `标签`
    * `hg tag 作品UNIX缩写_8_release_v年月日`
  1. 导师将团队仓库,加入主索引仓库的子仓库列表:
    * `http://code.google.com/p/kcpycamp/source/browse/.hgsub`

#### 标签格式规约 ####

```
[作品名]_[迭代数][_蟒营状态]_v[日期版本]
  |    |    |     |      |    +-- 使用 Ubuntu 的版本格式 yy.mm.dd
  |    |    |     |      +-- version ~ 版本前缀
  |    |    |     +-- 是否闭营终版,如果是,加入 _release
  |    |    +-- iterate次数,使用 i\d 格式,数字是第几次迭代的计数,从1开始
  |    +-- 各个字段使用下划线间隔
  +-- 团队作品的 UNIX 缩写名  
```
  * **注意!** ~ 标签除数字和下划线之外,只使用小写字母,不应该使用任何其它字符!


## 其它協作模型 ##

  1. [无政府状态](HgFlowAnarchy.md)
  1. [单一中央版本库](HgFlowCentralAlone.md)
  1. [托管的中央版本库](HgFlowCentreDepository.md)
  1. [使用多个分支工作](HgFlowBranchRepos.md)
  1. [特性分支](HgFlowBranchFeatures.md)
  1. [发布列车](HgFlowReleaseTrain.md)
  1. [Linux 内核模型](HgFlowLiunxKernel.md)
  1. [只读与共享写协作](HgFlowShaReadWrite.md)



**要牢记的因素**
  * 任何一种模型,其实都是`浮云`,作为团队管理者,必须关注的是人!
  * 团队里所有成员的真实能力和理解能力!
  * 因为,不论模型/流程,设计得再简单/明了/科学...要对团队協作起到正面作用,只能是**所有成员**的**每一次版本操作**都遵守了约定,否则,就会引发混乱/挫败/对抗...
  * 实效的团队協作模型的建立,最好是:
    1. 岗前培训,提供足够的时间,专心试用/训练/理解協作模型!
    1. 定期回顾仓库使用情况,识别非法操作/文件/标签/分支,及时清理和通告!
    1. 配合专门设计的 Hooks 脚本,进行自动化的识别/禁止/提醒/通告...

> PS::
    * [Juven Xu » 一个成功的Git分支模型](http://www.juvenxu.com/2010/11/28/a-successful-git-branching-model/)
      * [你为神马不用git-flow呢? | Jeff的妙想奇境](http://www.jeffkit.info/2010/12/860/)
    * 原[蟒营協作设计](HgFlowOldCamp.md)
      * [作品团队组长管理规约](HgTeaMana.md)
      * [蟒营导师仓库管理规约](HgCampMana.md)

# 参考 #
  * [WorkingPractices - Mercurial](http://mercurial.selenic.com/wiki/WorkingPractices)
    1. [Subrepositories - Mercurial](http://mercurial.selenic.com/wiki/Subrepositories)
    1. [MultipleCommitters - Mercurial](http://mercurial.selenic.com/wiki/MultipleCommitters)
  * [Steve Losh](http://stevelosh.com/about/)
    1. [Mercurial Workflows: Stable & Default / Steve Losh](http://stevelosh.com/blog/2010/05/mercurial-workflows-stable-default/)
    1. [Mercurial Workflows: Translation Branches / Steve Losh](http://stevelosh.com/blog/2010/06/mercurial-workflows-translation-branches/)
    1. [Mercurial Workflows: Branch As Needed / Steve Losh](http://stevelosh.com/blog/2010/02/mercurial-workflows-branch-as-needed/)
  * [WorkingWithSubversion - Mercurial](http://mercurial.selenic.com/wiki/WorkingWithSubversion)
  * http://hgtip.com/
    1. [Combining Repositories / hg tip](http://hgtip.com/tips/advanced/2009-11-17-combining-repositories/)



---


