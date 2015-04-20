[Hg](HgUsage.md),[協同模型](HgFlows.md)
:[无政府](HgFlowAnarchy.md)
|[单一中央](HgFlowCentralAlone.md)
|[托管中央](HgFlowCentreDepository.md)
|[分支仓库](HgFlowBranchRepos.md)
|[特性分支](HgFlowBranchFeatures.md)
|[发布列车](HgFlowReleaseTrain.md)
|[内核模型](HgFlowLiunxKernel.md)
|[写共享](HgFlowShaReadWrite.md)

# Hg工作流:无政府状态 #


参考: **[Mercurial 权威指南 第 5 章 团体协作](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/collaborating-with-other-people.html)**


## 概述 ##
是的,这一模型没人倡议使用! 但是,这的确是存在的一种模型:
  1. 在任何时间/地点/情景中,只要运行`hg serve -d` 就立即将本地仓库发布到网络中
  1. 组织现场的人,直接通过对本地仓库的下拉/上推,进行快速迭代式开发

## 操作 ##
  1. 启动本地web服务
    * 进入本地工作目录
    * 修订本地配置`.hg/hgrc`,追加:
```
[web]
push_ssl=False  #关闭 SSL 连接
allow_push=*    #允许他人推送修订
```
    * 启动仓库发布服务
```
hg serve -p 9002 -a 127.0.0.1 -n "HgDemo: BAR'srv. clone"
    |       |       |           |
    |       |       |           +-- 仓库描述
    |       |       +-- 绑定IP,一般修订成当前局域网IP
    |       +-- 绑定端口,尽量 9000 以上的,以免和其它本地服务冲突
    +-- 临时仓库服务发布
```
      * 通过浏览器就可以看到仓库
![http://kcpycamp.googlecode.com/files/zq_2010-09-27-174457_645x337_scrot.png](http://kcpycamp.googlecode.com/files/zq_2010-09-27-174457_645x337_scrot.png)
      * 甚至有所有修订的版本图谱!
![http://kcpycamp.googlecode.com/files/zq_2010-09-27-174509_653x361_scrot.png](http://kcpycamp.googlecode.com/files/zq_2010-09-27-174509_653x361_scrot.png)
  1. 同网段的其它成员就可以使用标准`拉-合并-提交`流程进行相互提交了!
    * 注意:
      1. 确保相互间的网络是通的,可以 ping 通!
      1. 要在 `[path]` 配置节增补临时发布的仓库
    * 使用标准`拉-合并-提交-发布`流程,合并不同仓库的代码到主线,例如
```
> hg pull -u http://127.0.0.1:9001/#10
   |   |   |        |               +-- 指定版本
   |   |   |        +-- 指定仓库的URL,本地或是远程
   |   |   +-- 下拉后立即更新本地代码
   |   +-- 同步远程仓库子命令
   +-- Hg 主操作命令
> hg merge
> hg ci -m "blalalala"
> hg push
```

## 蟒营建议 ##
  * 如果对 code.google/Bitbucket.org 等外网项目托管服务商的访问有问题时
  * 可以使用这种模型,进行本地团队的局域网协作
  * **但是!** 依然应该有统一的版本管理约定,比如说:
    1. 谁的仓库为主仓库,最后统一合并为团队稳定版本,定期上推到托管空间
    1. 统一使用 上推还是主持人拉的方式进行启动合并
    1. 各种分支/标签的命名规约
> > ...

简单的说,这种模型最适合于清醒的知道自个儿在作什么的团队!
  * 至少其中有一个非常熟悉 Hg 命令的主持人来带领大家享受随心的協作!


---

