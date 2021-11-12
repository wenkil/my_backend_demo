#### 系统地址：

###后台管理系统：[在线预览](http://122.51.128.27:8080/)

账号密码：用户名 test1 密码 abc123

#### 技术使用：

基于[Element-admin(基础版)](https://github.com/PanJiaChen/vue-admin-template) +  Express  + Mysql

#### 系统介绍：

系统模块：登录验证，权限管理，角色分配

客户模块：线索管理、客户列表、联系人、跟进记录

系统分析：客户分析、流程分析

产品模块：产品分类、产品列表

行政模块：部门管理、员工列表

订单列表：创建及审批功能

回款列表：创建及审批功能

#### 逻辑介绍：

**登录验证:** 由管理员配置账号密码,用户存在且非禁用状态方可登录	

**权限与角色:** 由管理员进行角色分配及权限分配，登录后台的用户无需退出登录，刷新页面即可更新最新权限列表

**上下级关系:** 不能设置自己为自己上级且自己的下级层级不能设置为上级

****

**以下页面使用上下级逻辑关联数据：当前登录用户只能查看或操作 [自己创建] 或 [自己是负责人] 的线索或客户数据及所有下属的相同规则的数据(管理员除外)**

**线索管理:** 录入线索名称及线索来源，责任人只可分配后台启用用户；线索转化：自动将数据同步到客户列表，并在客户分析页面展示已转化客户分析图

**客户列表:** 展示客户基本信息及联系人、跟进记录、订单等详细信息

**联系人:**  新建联系人须关联客户，否则无法创建；列表：展示联系人基本信息

**跟进记录:**  创建跟进记录,只能选择客户联系人进行跟进,点击列表中的联系人信息显示详细客户信息

------

**客户分析:**  客户的来源、等级、行业分析图

**流程分析：** 开发中~~~

****

**产品分类:**  按照层级新建分类，每一级的类名皆不可重复，已被关联产品的分类不可删除，删除后的产品同样不能新建产品

**产品列表:**  新增时只能关联未被删除且层级为四级的产品分类；禁用产品不可新增订单,已关联的订单可以看到该产品详情

****

**部门管理:**   最大可建四级部门。删除部门时需转移部门下的员工，否则不可删除

**员工列表:**   展示员工基础信息及入职、离职、试用期状态下的所有人数

****

**订单列表：** 

- 订单周期: 未取消,已取消

- 订单审批状态: 待审批,已驳回,已通过

- 订单生效状态：已生效,未生效

- 新建订单只能创建当前操作用户为客户负责人的订单，

-  新建订单逻辑： 只能选择启用产品，审批人可选1-3位且不可选择自己

- 订单列表：只能查看自己创建的和待我审批的两种类型订单，在此基础上查看其他状态筛选订单

- 订单审批：根据审批人顺序审批，上一级未审批时，不展示审批按钮。

- 审批结果：审批通过则进行下一级审批人继续审批(如无下级审批，则状态改为审批通过)，审批驳回则订单需重新编辑提交审核，重新走审核流程且记录每次审批操作，在订单详情里展示

- 取消订单：订单没有创建回款可立即取消,如已有回款走下面流程：

  ```tex
  如果创建了n笔回款，并且都没有通过,提示需要删除所有回款后才可取消
  如有任一一笔回款通过，不可取消订单(走退款流程)
  如果订单生效,不能取消
  ```

**回款列表：**

- 审批状态及生效状态同订单状态
- 订单状态为待审批即可创建回款
- 回款审批时订单必须为审批通过状态才可审批回款，且根据审批人顺序审批，上一级未审批时，不展示审批按钮
- 审批结果：逻辑同订单审批结果相同
- 回款取消：只有自己创建的回款,并且审批尚未通过才可以取消，审批通过后的回款只能走退款流程

------

**退款功能：** 开发中~~~
