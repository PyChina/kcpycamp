[Hg](HgUsage.md),[協同模型](HgFlows.md)
:[无政府](HgFlowAnarchy.md)
|[单一中央](HgFlowCentralAlone.md)
|[托管中央](HgFlowCentreDepository.md)
|[分支仓库](HgFlowBranchRepos.md)
|[特性分支](HgFlowBranchFeatures.md)
|[发布列车](HgFlowReleaseTrain.md)
|[内核模型](HgFlowLiunxKernel.md)
|[写共享](HgFlowShaReadWrite.md)

# Hg工作流:只读与共享写协作 #


参考: **[Mercurial 权威指南 第 5 章 团体协作](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/collaborating-with-other-people.html)**


## 概述 ##
这是一般集中式版本仓库无法同时提供的两种协作模式:
  1. 仓库只读,其它人只能下载到最新版本
  1. 仓库可写,接受其它人的修订上推

但是, Hg 就能够同时支持这两种模式,在同一工程中!
  * 因为,是 [DVCS](AbtDvcs.md) 哪!
  * 每一个仓库克隆都是完全意义和功能上的仓库
  * 就算团队仓库托管在 bitbucket.org 上配置为只读时
  * 我们依然,可以在本地将克隆下来的仓库,通过`hg serve` 在局域网以可写模式共享出来!


> 常见的情景是::
    * 在旅中,团队想抓紧时间进行开发
    * 需要協同时,使用 [单一中央](HgFlowCentralAlone.md)或是[内核模型](HgFlowLiunxKernel.md) 进行交流
    * 只要简单的将组长的本地仓库发布出来就好:
      1. 可以使用 web 方式
      1. 也可以使用共享目录方式
      1. 进一步的,出于安全考虑,也可以通过 ssh 协议进行远程目录访问




---


