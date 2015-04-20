**PythoniCamp**::[目标](GoalPythoniCamp.md)![参与](HowtoJoin.md);[流程](KcPyCampFlow.md);[作品](PythoniCampItems.md):[开发](HowtoDevelop.md);[资源](PythonicRes.md);[讨论](HowtoDiscuss.md);[SCM](HowtoScm.md);[测试](HowtoTesting.md)...


# Hg作品集锦式代码管理 #
`面向蟒营的Commitor ~即导师们的作品团队代码发布管理规约`

基于 DVCS 态度的**个人-团队-工程**代码協同流程,详细参考::
  * [作品团队组长管理规约](HgTeaMana.md)
  * [蟒营导师仓库管理规约](HgCampMana.md)
  * [常见Hg協同流程简介](HgFlows.md)

## 流程説明 ##
`旧蟒营協同设计,已经简化不再使用以下约定`
```
定义:
    + 蟒营成品库 https://kcpycamp.googlecode.com/hg/
    + 作品初始库 https://initial.kcpycamp.googlecode.com/hg/
    + 作品团队库 https://u-item.kcpycamp.googlecode.com/hg/
                       |  +-- 作品UNIX缩写名
                       +-- 团队组长 Gmail 帐号名
    + 作品成员库 https://my-u-item.kcpycamp.googlecode.com/hg/
                       |  |   +-- 作品UNIX缩写名
                       |  +-- 团队组长 Gmail 帐号名
                       +-- 成员 Gmail 帐号名
```

### 0:为团队作品建立成员接入点 ###
  1. 在本地clone 成品仓库,e.g:
    * `hg clone https://kcpycamp.googlecode.com/hg/ kcpycamp-trunk`
  1. 从作品团队库,clone 作品到对应子目录,e.g:
    * `hg clone https://u-item.kcpycamp.googlecode.com/hg/ item`
  1. 聲明子仓库:
    * 编辑 `.hgsub` 文件,e.g:
    * `item = https://u-item.kcpycamp.googlecode.com/hg/`

### 1:定期发布团队作品迭代版本 ###
  1. 每周,或是约定的迭代版本发布日期时,输出团队作品最新代码e.g:
```
$ cd /path/2/kcpycamp/item
$ hg pull -u
...
```
  1. 标签后,检入成品仓库e.g:
```
$ hg tag item_i1_v10.11.11
$ hg push
```

### 2:结项发布团队作品闭营终版 ###
  1. 闭营时,检出团队作品`封版`代码e.g:
```
$ cd /path/2/kcpycamp/item
$ hg pull -u
...
```
  1. 标签后,检入成品仓库e.g:
```
$ hg tag item_i5_camped_v11.01.11
$ hg push
```


## 标签格式规约 ##

```
[作品名]_[迭代数][_蟒营状态]_v[日期版本]
  |    |    |     |      |    +-- 使用 Ubuntu 的版本格式 yy.mm.dd
  |    |    |     |      +-- version ~ 版本前缀
  |    |    |     +-- 是否闭营终版,如果是,加入 _camped
  |    |    +-- iterate次数,使用 i\d 格式,数字是第几次迭代的计数,从1开始
  |    +-- 各个字段使用下划线间隔
  +-- 团队作品的 UNIX 缩写名  
```
  * **注意!** ~ 标签除数字和下划线之外,只使用小写字母,不应该使用任何其它字符!


# 参考 #

  * [UnderstandingMercurial - Mercurial](http://mercurial.selenic.com/wiki/UnderstandingMercurial)
  * **[子仓库](http://mercurial.selenic.com/wiki/ChineseSubrepository)**
    * [NestedRepositories - Mercurial](http://mercurial.selenic.com/wiki/NestedRepositories)
    * [ForestExtension - Mercurial](http://mercurial.selenic.com/wiki/ForestExtension)






---


