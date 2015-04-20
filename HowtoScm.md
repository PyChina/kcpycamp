**PythoniCamp**::[目标](GoalPythoniCamp.md)![参与](HowtoJoin.md);[流程](KcPyCampFlow.md);[作品](PythoniCampItems.md):[开发](HowtoDevelop.md);[资源](PythonicRes.md);[讨论](HowtoDiscuss.md);[SCM](HowtoScm.md);[测试](HowtoTesting.md)...

# SCM #
~ Software Configuration Management


## 概述 ##
软件配置管理!
  * 参考:[恼人不休的问题：什么是软件配置管理？](http://blog.csdn.net/bvbook/archive/2008/06/03/2507545.aspx)

简单的说:
  * 就是对在软件开发过程中一切有利于提高软件质量的物件进行一致性的管理
  * 这些物件就是`配置项`
  * 所谓管理,就是统一的标识/版本|变更|发布控制,确保一切`配置项`:
    * 可标记
    * 可追踪
    * 可改进

通俗的理解就是:
  * 在开发过程中一切有意思的信息/文件/数据 都得通过工具/规范/流程 变成团队资产,令所有人合理使用!

最简单和直观的SCM就是:
  * 一切开发行为,统一在版本仓库中进行自动记录;
  * 版本仓库是种方便/神奇的时间仓库:
    1. 自动将所有人的所有修订全部记录下来
    1. 所有修订,所有人可以随时追查
    1. 可以安全的将任何代码恢复到指定的任何历史状态中
    1. 可以安全的隔离个人代码的**实验状态**和软件正式版本代码的**发布状态**

**习惯并坚持运用SCM工具来辅助开发,是成长为一名[靠谱](http://wiki.woodpecker.org.cn/moinKaoPulity)的程序员的必经之路!**


## 版本控制 ##
  * [有关DVCS](AbtDvcs.md) <sup>理解分布式版本控制基本原理</sup>
  * **[Hg使用](HgUsage.md)** <sup>日常蟒营版本仓库使用</sup>

**为什么要使用版本仓库来记录所有代码/文档的变化?!**
  1. 将自个儿对团队的贡献逐一记录在案,形成历史证据
  1. 如果交付时,出现严重问题,有足够的历史痕迹可以追查是何时,谁引入了什么代码引发的
  1. 进一步的,如果没有一个真实的工程推进的历史的话,团队自身也没有一个客观的代码开发效率参考,来判定自身的状态

> 总之,使用一个公开的,自动化的,安全的,不可修改的,客观的版本仓库,将工程中涉及的所有智力劳动成果的所有变化记录下来,是软件开发比其它任何工作,都要靠谱的一个因素,使用起来,坚持下去,才可以受益无穷,如果仅仅因为当前自个儿直觉的判定说无用,而不去用,形成了不良的开发习惯后,受苦的,以后也只有是自个儿...

### 放弃 code.google ###
  * 原先使用 SVN 进行团队協同,发现很多问题:
    1. 开发目录污染...`.svn` 无处不在
    1. 作品目录繁多,容易输出错
    1. 集中式版本管理,离线不可用! 抢先检入...
  * 但是,在 code.google 中,迁移为 Hg 仓库后
    * ![http://kcpycamp.googlecode.com/files/zq_2011-04-01-110947_629x343_scrot.png](http://kcpycamp.googlecode.com/files/zq_2011-04-01-110947_629x343_scrot.png)
    * 不久就经常出现以上问题
    * 而且,限定每个工程,最多只能创建 8 个仓库

综合以上历史,我们进一步选择了 [Bitbucket.org](https://bitbucket.org)专业 Hg 仓库托管!


## 参考 ##
**为什么选择 Hg**
  1. [翻譯-Git 與 Mercurial 的分析 « TWPUG::Kiang](http://blog.twpug.org/416) <sup>Google的分析对比</sup>
  1. [PEP 374 -- Choosing a distributed VCS for the Python project](http://www.python.org/dev/peps/pep-0374/) <sup>Python 的分析对比</sup>

**敏捷模式**
  1. [InfoQ: 敏捷初哥忏悔录](http://www.infoq.com/cn/articles/agile-confessions-sharma)



---

TOC: 