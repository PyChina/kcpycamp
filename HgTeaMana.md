**PythoniCamp**::[目标](GoalPythoniCamp.md)![参与](HowtoJoin.md);[流程](KcPyCampFlow.md);[作品](PythoniCampItems.md):[开发](HowtoDevelop.md);[资源](PythonicRes.md);[讨论](HowtoDiscuss.md);[SCM](HowtoScm.md);[测试](HowtoTesting.md)...



# Hg分布式团队協同 #
`和每期蟒营各个作品团队组长规约日常开发中的版本仓库事务!`

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
    + 成员工作库 https://my-u-item.kcpycamp.googlecode.com/hg/
                       |  |   +-- 作品UNIX缩写名
                       |  +-- 团队组长 Gmail 帐号名
                       +-- 成员 Gmail 帐号名
```

### 作为团队管理者的操作 ###
> 职责::
    1. 开辟团队作品仓库
    1. 辅助成员逐一建立个人作品开发仓库
    1. 定期同步/合并/解决成员代码冲突,发布团队作品稳定代码
    1. 向成品仓库通知迭代版本代码
    1. 向成员仓库通知`封版`代码


> 操作::
    1. 团队成立后,设计/认领作品后,明确作品的E文全称,并協商确认 UNIX 缩写~<sup>全小写字母,除数字和下划线,不包含其它字符</sup>
    1. 为团队创建作品仓库:
      1. 使用Gmail 帐号登录 http://code.google.com/p/kcpycamp;
      1. 进入 `Source`-> [initial仓库](http://code.google.com/p/kcpycamp/source/checkout?repo=initial)
      1. 点击`Create your own clone`创建作品仓库,访问地址形如:
```
               https://u-item.kcpycamp.googlecode.com/hg/
                       |  +-- 作品UNIX缩写名
                       +-- 团队组长 Gmail 帐号名
```
      1. 在本地克隆团队仓库.e.g:
        * `hg clone https://u-item.kcpycamp.googlecode.com/hg/ item`
      1. 为团队作品创建自述文件,并检入仓库,提交服务端:
```
$ cd /path/2/item
$ vi readme.txt
...
```
        * 格式形如:
```
作品名

设计文档: URL
团队成员:
 + 姓名 Gmail
 + ...
开发计划:
 + 迭代一期 日期,目标
 + 迭代二期 日期,目标
 + ...

变更记要:
 101111 谁,作了什么重要变更
```
        * 然后,完成本地检入,和向远端仓库推送:
```
$ hg add
$ hg ci -m "初始化 item 作品仓库"
$ hg push
正在推到 https://teamleader:***@teamleader-foo.googlecode.com/hg/
正在搜索修改
遠端: Success.
...
```
    1. 指导其它成员建立工作仓库:
      * **注意!**
        * 团队组长必须先建立好团队仓库,
        * 并且完成自述文档<sup>readme.txt</sup>建立并提交成功后,
        * 成员才可以创建个人工作仓库!
      * 通知团队成员,逐一登录并创建服务端团队仓库的克隆
      * 确认团队成员,都在本地克隆了对应的个人工作仓库
    1. 收集,并在本地配置好所有成员的个人工作仓库别名:
      * 修订本地仓库的`.hg/hgrc`文件类似:
```
[paths]
default =  https://teamleader:Ub3mB7Wa5tm4@teamleader-foo.googlecode.com/hg/
                    |        |  |         |   |        +-- 作品UNIX缩写
                    |        |  |         |   +-- 组长本人邮箱名
                    |        |  |         +-- 身份认证和真实仓库URL 分隔符
                    |        |  +-- 组长本人的 CodeGoogle 口令
                    |        +-- 帐号和口令间隔符
                    +-- 组长本人邮箱名
A =  https://memberA-teamleader-foo.googlecode.com/hg/
|               |       +-- 团队仓库名(含组长邮箱帐号)
|               +-- 团队成员自个儿的 Gmail 邮箱帐号
+-- 组长自定的成员仓库别名
B =  https://memberB-teamleader-foo.googlecode.com/hg/
..
```
    1. 定期<sup>比如说:每日 21:00</sup> 检查所有成员仓库,合并代码,e.g:
```
$ cd /path/2/item
$ hg in A
...
$ hg in B
...
$ hg ci -m "解决所有冲突,发布当日团队最新代码"
...
```
    1. 按计划,定期发布团队作品迭代版本:
      * 完成成员代码的合并
      * 并共同测试所有目标特性
      * 增补团队仓库根目录的 `readme.txt` 自述文档,增补本次完成的特性描述,和重要的其它变更/修订
      * 向蟒营列表 [kcpycamp@googlegroups.com](mailto:kcpycamp@googlegroups.com?subject={item=release}) 发送邮件説明迭代版本已经发布,以及当前版本的 URL


### 作为团队成员的操作 ###
> 职责::
    1. 按时完成开发任务,确认自个儿的代码可用
    1. 提交前同步团队代码,解决冲突
    1. 检入时,要写足够清晰/有用的检入注释
    1. 帮助其它成员理解自个儿的代码


> 操作::
    * 同 **[HgUsage](http://code.google.com/p/kcpycamp/wiki/HgUsage#%E6%97%A5%E5%B8%B8%E4%BD%BF%E7%94%A8:)**<sup> - kcpycamp - Pythonic Hg使用 - Project Hosting on Google Code</sup>








---

TOC: 
