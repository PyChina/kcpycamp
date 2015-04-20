**PythoniCamp**::[目标](GoalPythoniCamp.md)![参与](HowtoJoin.md);[流程](KcPyCampFlow.md);[作品](PythoniCampItems.md):[开发](HowtoDevelop.md);[资源](PythonicRes.md);[讨论](HowtoDiscuss.md);[SCM](HowtoScm.md);[测试](HowtoTesting.md)...


# Hg精简手册 #




当前 PythoniCamp 选择 [Hg(Mercurial,水银)](http://mercurial.selenic.com/) 作为版本仓库

## 环境约定 ##
### 作品索引仓库 ###
URL: **https://kcpycamp.googlecode.com/hg/**
  * clone 仓库不用任何授权,使用[Mercurial工具](http://mercurial.selenic.com/downloads/)即可,推荐**TortoiseHG** <sup>M$中的同学</sup>
  * 收集各期蟒营的成品项目代码, **不用作当期蟒营的开发協同仓库!**
  * 合并相关项目代码变更到主仓库,需要:
    1. 向[导师团](PythoniCampTutors.md) 发出说明邮件
    1. 等待评审通过,由`导师`完成子仓库追加

### 团队开发仓库 ###
`各期蟒营中,各个作品团队专用的協同仓库`


**创建过程**
  1. 导师绝初始化仓库,获得类似访问URL:
```
https://bitbucket.org/ZoomQuiet/pycamp.***
         |              |       |       +-- 作品的UNIX缩写
         |              |       +-- 统一前缀
         |              +-- 由导师统一开辟
         +-- bitbucket.org 进行托管
```
  1. 由团队组长,自行注册 https://bitbucket.org 反馈导师 `注册帐号`
  1. 导师绑定团队组长对应仓库管理权限后,由组长自行绑定同组成员的帐号到仓库中

## 安装 Hg ##
在M$环境中:
  1. 下载 [Mercurial工具](http://mercurial.selenic.com/downloads/)<sup>对应CPU型号的!</sup>
  1. 配置语言环境
  1. 初始化用户信息

**不论任何时候,都建议尽可能通过命令行来进行操作!**
  1. 正当理解操作行为
  1. 形成良好操作流程
  1. 积累肌肉记忆,远离鼠标的低效率操作,节省时间,享受生命!

![http://kcpycamp.googlecode.com/files/zq_2010-11-09-153203_504x86_scrot.png](http://kcpycamp.googlecode.com/files/zq_2010-11-09-153203_504x86_scrot.png)
  * 文本的提示非常人性化.,..



## 日常使用: ##
`提示成员平时的仓库使用流程中最常见的操作`
> 视频教程:
    1. [初始化本地克隆以及配置后无口令push](http://zoomquiet.org/res/m/v/pythonicamp/110411-pyicamp-hg-0-clone-ci-push.htm)


### 0:初始化 ###
  1. 自行注册 [bitbucket.org](https://bitbucket.org/)
    * 并由组长绑定仓库权限
  1. 在本地合适的目录,克隆团队工程仓库:
```
> hg clone https://bitbucket.org/ZoomQuiet/pycamp.***
  |     |   |       +-- 仓库URL,由导师统一开辟
  |     |   +-- 使用SLL 加密 HTTP 协议
  |     +-- 克隆子命令
  +-- Hg 主命令
```
  1. 本地用户配置
    * 进入仓库所在目录的 `.hg` 隐藏目录
    * 编辑 `hgrc` 文本文件,类似:
```
[ui]
username = You Name <you.mailbox@gmail.com>
[paths]
; 可以在这儿嵌入认证信息,以免每次都要输入,比如说/:
default = https://帐号名:口令@bitbucket.org/ZoomQuiet/pycamp.***
                     | | | +-- 使用 @ 缀上仓库URI
                     | | +-- 注册时自行设定的口令
                     | +-- 使用 : 间隔帐号和口令
                     +-- 你的 bitbucket帐号名,一般使用 gmail 邮箱名
[hostfingerprints]
bitbucket.org = 81:2b:08:90:dc:d3:71:ee:e0:7c:b4:75:ce:9b:6c:48:94:56:a1:fe
```

### 1:本地修订 ###
  1. 追加文件到Hg仓库中,常用命令:
    * `hg add /path/2/filename` <sup>可以使用正则表达式批量加入文件</sup>
  1. 从Hg仓库中清除文件,常用命令:
    * `hg remove /path/2/filename` <sup>清除后,得提交 ci 后才生效</sup>
  1. 检入本地修订,常用命令:
    * `hg revert --all` <sup>检入前反悔</sup>
    * `hg ci -m "提交日志说明..."` <sup>检入的一般命令输入</sup>
  1. 仓库状态探查:
    1. `hg parent` <sup>查阅最新版本</sup>
    1. `hg log -l 3` <sup>查阅最近三个版本</sup>
    1. `hg status` <sup>查阅仓库整体状态</sup>
    1. `hg st` <sup>简写</sup>
```
> hg st
M HgUsage.wiki
? TortoiseMerge.wiki

会列出所有自动发现的文件变动,并通过前缀代码进行标识,所有标识的含义:
      M = modified  已修订
      A = added     已追加(但还没有提交的)
      R = removed   已清除(但还没有提交的)
      C = clean     已清除
      ! = missing (deleted by non-hg command, but still tracked)
                    丢失中(用系统命令或是其它方式删除,但是在Hg 依然追踪的文件)
      ? = not tracked 未加入 Hg 追踪的文件
      I = ignored   已忽略
```



### 2:解决冲突 ###
  1. 标准`拉-合并-提交`本地开发流程
    1. 探查远程仓库,常用命令:
      * `hg incoming` <sup>顯示來源端新的 变更集!</sup>
        * `hg in` <sup>简写</sup>
      * `hg outgoing` <sup>顯示目的端沒有的 变更集!</sup>
        * `hg out` <sup>简写</sup>
      * 如果配置了`[paths]`中不同的仓库,就可以使用上述命令随时探查不同仓库的变化
    1. 下拉同步远程修订,常用命令:
      * `hg pull -u` <sup>下载并更新本地代码克隆</sup>
```
> hg pull -u
pulling from http://10.20.208.13:8000/
searching for changes
adding changesets
adding manifests
adding file changes
added 1 changesets with 1 changes to 1 files (+1 heads)
not updating, since new heads added
(run 'hg heads' to see heads, 'hg merge' to merge)
```
        * 如果远程仓库有变更,将有提及,照办就好
      * `hg heads` <sup>代码分支观察</sup>
```
> hg heads
changeset:   23:016b59e9f457
tag:         tip
parent:      20:4374f5ca86ad
user:        Zoom Quiet <Zoom.Quiet@gmail.com>
date:        Tue Sep 28 11:28:20 2010 +0800
summary:     main REPO.:M$ test meger

changeset:   22:7d2a431e2154
parent:      21:2f0443e974f6
parent:      20:4374f5ca86ad
user:        Bar <bar+locfoo@gmail.com>
date:        Tue Sep 28 11:25:37 2010 +0800
summary:     Bar: M$ merged by BC3
```
        * 可以观察到变更集有两个最新状态标签,代表来自两个分布式仓库的最新代码,其中:
          1. tag: tip 代表这是本地的最新代码
          1. parent 指出了代码变更的依据版本是哪个/些
          1. changeset 就是变更集,由两部分组成:
```
changeset:   22:7d2a431e2154
              |     +-- 全球唯一的Hash ID,代表任意仓库的具体一个变更集
              +-- 整数,本地仓库的变更集自增ID
```
    1. 合并本地修订变更,常用命令:
      * `hg merge`
      * 系统将调用默认,或是指定的差异管理工具,进行合并,如果需要将弹出界面,人工测定怎么合并
      * 推荐乌亀系列专用合并器:**TortoiseMerge** ~ <sup>开源免费的轻便差异管理工具!</sup>
        * 配置中可选:
        * ![http://kcpycamp.googlecode.com/files/ZQshutter_100928-170913_001.png](http://kcpycamp.googlecode.com/files/ZQshutter_100928-170913_001.png)
      * UTF-8 中文显示正常:
        * ![http://kcpycamp.googlecode.com/files/zq_2010-09-28-172658_903x333_scrot.png](http://kcpycamp.googlecode.com/files/zq_2010-09-28-172658_903x333_scrot.png)
      * **注意!**~默认的跨平台差异管理工具 kdiff3 对于中文支持很囧!建议不要使用...
        * 需要先安装 [TortoiseSVN](http://tortoisesvn.net/downloads)<sup>TortoiseMerge 是内置在其中的一个辅助工具</sup>
        * 也可以直接在仓库配置中声明:
        * 本地仓库所在目录的 .hg/hgrc 中追加
```
[ui]
merge = tortoisemerge

[tortoisehg]
vdiff = tortoisemerge
```
    1. 提交修订到工作仓库,常用命令:
```
> hg ci -m "Bar: M$ merged by BC3 for snap"
  |   |  |  +-- 提交日志,尽可能的明确说明这次提交解决了什么
  |   |  +-- 日志前导子命令
  |   +-- commit 的简写
  +-- Hg 主操作命令
```
    1. 发布修订到远程仓库,常用命令:
```
> hg push
pushing to http://10.20.208.34:9002/
searching for changes
note: unsynced remote changes!
remote: adding changesets
remote: adding manifests
remote: adding file changes
remote: added 2 changesets with 2 changes to 1 files
```
      * 可以从对应仓库的图形化版本变更图谱中观察到对应的变化!
        * ![http://kcpycamp.googlecode.com/files/ZQshutter_100928-114330_graph.png](http://kcpycamp.googlecode.com/files/ZQshutter_100928-114330_graph.png)
        * ![http://kcpycamp.googlecode.com/files/ZQshutter_100928-114402_cset.png](http://kcpycamp.googlecode.com/files/ZQshutter_100928-114402_cset.png)
    1. 回退修订,常用命令:
      * `hg revert -a -r3` <sup>检入后反悔,恢复到指定版本!</sup>

**注意**:
  1. Hg **不追踪目录!**




## 团队协作: ##
基于 DVCS 态度的**个人-团队-工程**代码協同流程,详细参考::
  * [常见Hg協同流程简介](HgFlows.md)

### 整体流程 ###
  1. <sup>团队组长:</sup> 认领 bitbucket.org 团队仓库,并分配成员权限
  1. <sup>团队成员:</sup>
    * 初始化本地仓库,并完成约定的配置
    * 尽情的开发和及时检入本地仓库
    * 定期发布修订到团队仓库
  1. <sup>蟒营导师:</sup> 闭营时,追加到主索引仓库

### 内网協同 ###
`由于 Hg 是标准的分布式仓库,完全可以通过局域网直接进行协同!`

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




## 参考 ##
**为什么选择 Hg**
  1. [[翻譯](http://blog.twpug.org/416)Git 與 Mercurial 的分析 « TWPUG::Kiang] <sup>Google的分析对比</sup>
  1. [PEP 374 -- Choosing a distributed VCS for the Python project](http://www.python.org/dev/peps/pep-0374/) <sup>Python 的分析对比</sup>

**Hg的文档**
  1. ["版本管理及SVN使用初探"](http://www.zoomquiet.org/share/s5/0702-VMnSVN/)<sup>S5 幻灯</sup>ZoomQuiet SCM思想简介
    1. [中文教育 - Mercurial](http://mercurial.selenic.com/wiki/ChineseTutorial)<sup>官方速成教程</sup>
      * **[Hg使用速查表](http://wiki.woodpecker.org.cn/moin/ZqCcHgCheatSheet)**
    1. [Mercurial 权威指南](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/index.html)<sup>官方大全</sup>
      * [第 8 章 发布管理与分支开发](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/managing-releases-and-branchy-development.html)
    1. [Mercurial: The Definitive Guide](http://hgbook.red-bean.com/read/)~<sup>Bryan O'Sullivan</sup>写的深入浅出式教程
    1. [Hg Init: a Mercurial tutorial](http://hginit.com/top/)<sup> by Joel Spolsky</sup>伟大的Joel写的教程!

**Hg的技巧**
  1. [MercurialFAQ](http://code.google.com/p/support/wiki/MercurialFAQ)<sup>Project Hosting on Google Code</sup>支持文档
    1. [TortoiseHg中文文件名乱码解决 | 我自然](http://www.yankay.com/tortoisehg%e4%b8%ad%e6%96%87%e6%96%87%e4%bb%b6%e5%90%8d%e4%b9%b1%e7%a0%81%e8%a7%a3%e5%86%b3/?variant=zh-cn)
  1. [OtherTools - Mercurial](http://mercurial.selenic.com/wiki/OtherTools) <sup>更多支持Hg 的工具</sup>
  1. hg 命令帮助查询,常用命令:
    * `hg help`
    * 可以根据疑问后綴相关命令,比如说
```
> hg help init
hg init [-e CMD] [--remotecmd CMD] [DEST]

create a new repository in the given directory

    Initialize a new repository in the given directory. If the given directory does not exist, it will be created.

    If no directory is given, the current directory is used.

    It is possible to specify an "ssh://" URL as the destination. See 'hg help urls' for more information.

选项:

 -e --ssh        指定要使用的 'ssh' 命令
    --remotecmd  指定要在远程运行的 'hg' 命令

使用 "hg -v help init" 显示全局选项
```

### 为何要创建服务端克隆? ###
[Why should I create a server-side clone?¶](http://code.google.com/p/support/wiki/MercurialFAQ#Why_should_I_create_a_server-side_clone?)
  * 用户克隆只是工程仓库的复本,任何人都可以随时创建;并不需要工程主持的许可;
  * 用户克隆也经常需要发布修订到工程仓库,以及从本地分享修订给其它用户; 如果直接提交修订到工程仓库,将引发所有相关用户的下拉-合并活动;
  * 用户克隆并不是分支,而且传统上也不是分支中的所有变更都要合并到主线上来;毕竟 Hg 是种分布式版本控制系统,推荐的贡献发布流程是由主持人 **下拉** 用户克隆中的变更,如果认同这次修订的话,再由主持人发布到主线中!
    * 这远比通过邮件传递补丁要轻松的多
    * 不论主持人还是贡献者,都使用同一工具和界面来自然的完成 ;-)
  * 所以,只要你有 Gmail 帐号,就可以在 code.google 工程页面,创建服务端克隆,以便主持人进行评审接纳修订!



---

TOC: 
