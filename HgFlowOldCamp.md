# 蟒营Hg工作流 #

参考: **[Mercurial 权威指南 第 5 章 团体协作](http://i18n-zh.googlecode.com/svn/www/hgbook/zh/collaborating-with-other-people.html)**

```
  +---------------------+
  | member dev dir      +--------\  成员本地工作目录::
  | /path/2/kcpycamp    |        |  hg add      追加监控文件
  | or                  |        |  hg remove   清除文件监控
  | X:\path\2\kcpycamp  |        |  hg revert   反悔修订
  +---------------------+        |  hg ci       提交修订
                                 |  ...
                +----------------V--------+
                | member local REPOSITORY +------\  成员本地仓库::
                | /path/2/kcpycamp/.hg    |      |  .hg/hgrc (中配置默认发布仓库)
                | or                      |      |  [paths]
                | X:\path\2\kcpycamp/.hg  |      |  default-push = https://p1-kcpycamp.googlecode.com/hg/
                +--^---------------------+       |  (p1 成员名,在创建服务端克隆时自行指定)
                   ^                             |  
                   | .hg/hgrc                    |  hg push ... 发布修订到私人仓库克隆
                   | [paths]                     |  
                   | default = https://t1-kcpycamp.googlecode.com/hg/
                   | (t1 是团队/模块/子项目名,在创建服务端克隆时指定)
                   |                             |  
                   |                             |  
                   |                             V         
                   |               +-------------V-------------------------+
                   |               | REPOSITORY clone for self             |
                   |               | https://p1-kcpycamp.googlecode.com/hg/|
                   |               +--+------------------------------------+
                   |                  | 
                   |                  | 由团队小组长负责:
                   |                  | + pull 各个成员修订到团队/模块/子项目仓库克隆
                   |                  | + 并及时合并可能的冲突代码
                   |                  | 
                   |                  | hg merge ...
                   |                  V
         +---------+------------------V----------+
         | REPOSITORY clone for team             |
         | https://t1-kcpycamp.googlecode.com/hg/|
         +------------------------------------+--+
                                              |
                                              | 由工程主持人负责:
  +------------------------------------+      | + 定期汇总各个团队的阶段成果
  |main REPOSITORY                     <<<<---/ + 根据情况标定版本分支,组织发布
  |https://kcpycamp.googlecode.com/hg/ |
  +------------------------------------+

```





---


