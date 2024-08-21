# Talent天赋社区建设方案

V1.0.0

# 系统介绍
灵光一闪的idea, 做这样的一个社区平台, 旨畅游在互联网上的人们有一个地方能够社交, 在这个系统里, 发布文章, 分享一切. talent围绕着宇宙作为运营基础, 根据宇宙发布帖子, 不同的职场/生活/兴趣都能在这找到志同道合的朋友. 另外在talent里, 架设了自由职业/远程办公板块, 作者认为: 自由职业是未来灵活就业的趋势, 是未来人们的工作模式, 为人们带来自由, 同时给人带来自我约束, 专注的提升, 工作中也伴随着生活的点滴
自由职业伴随的是随时随地的办公, 随时随地的休息, 弹性的收入, 与生活平衡, 不用再看今天是不是工作日, 随时随地想去哪办公就去哪办公, 不用担心领导看到你电脑屏幕在浏览知乎或者微博, 不用在意早晚高峰与该死的通勤, 不用节假日去旅行的时候看着人山人海遍地人头, 管束自己的专注力与执行力, 为自己争取时间
远程办公意味着你可以有一份稳定的收入, 相对于自由职业, 收入这块不用担心, 具备着自由职业一切的好, 还稳定, 你说气不气呢



# 设想
Talent「天赋」在未来, 给更多人提供稳定自由的就业环境, 充实自由的生活, 在Talent上发挥自己的文笔, 成交自己的客户, 提升自己的能力, 提升幸福感

**Talent, 未来已来!!!**


# 建设步骤

以下建设步骤先后排序, 内容包括项目的架构, 技术, 流程, 需求

## 系统架构

### 后端

#### 框架选型与版本

|         版本号          |       技术框架 |
|:--------------------:|:----------:|
| Spring Cloud Alibaba | 2023.0.1.0 |
|     Spring Boot      |      3.3.0 |
|        Seata              |     2.0.0       |
|           Nacos           |    2.3.2        |
|          Hutool            |   5.8.28         |
|            Mybatis-plus          |   3.3.2         |
|             Pagehelper         |      2.1.0      |
|           Captcha           |     1.3.0       |
|             Knife4j         |     4.4.0       |
|             Elasticsearch         |     7.17.21       |
|               Minio       |      8.2.2      |
|              RocketMQ        |    2.3.0        |
|              Weixin        |     4.6.0       |
|       Fastjson               |    1.2.83        |
|          Fastjson2            |    2.0.51        |
|          Aspectjweaver            |   1.9.22.1         |
|                      |            |


#### 后端业务扭转流程及组件模型

![后端业务扭转与组件模型](..%2Fimage%2FdesignDocumentImage%2Fmodel1.jpg)


- VO（View Object）：显示层对象，通常是 Web 向模板渲染引擎层传输的对象。
- DTO（Data Transfer Object）：数据传输对象，前端像后台进行传输的对象，类似于param。
- BO（Business Object）：业务对象，内部业务对象，只在内部传递，不对外进行传递。
- Model：模型层，此对象与数据库表结构一一对应，通过 Mapper 层向上传输数据源对象。
- Controller：主要是对外部访问控制进行转发，各类基本参数校验，或者不复用的业务简单处理等。为了简单起见，一些与事务无关的代码也在这里编写。
- FeignClient：由于微服务之间存在互相调用，这里是内部请求的接口。
- Controller：主要是对内部访问控制进行转发，各类基本参数校验，或者不复用的业务简单处理等。为了简单起见，一些与事务无关的代码也在这里编写。
- Service 层：相对具体的业务逻辑服务层。
- Manager 层：通用业务处理层，它有如下特征：
  - 1） 对第三方平台封装的层，预处理返回结果及转化异常信息，适配上层接口。
  - 2） 对 Service 层通用能力的下沉，如缓存方案、中间件通用处理。
  - 3） 与 DAO 层交互，对多个 DAO 的组合复用。
- Mapper持久层：数据访问层，与底层 MySQL进行数据交互。
- Listener：监听 `RocketMQ` 进行处理，有时候会监听`easyexcel`相关数据。

关于`FeignClient`，由于微服务之间存在互相调用，`Feign` 是http协议，理论上是为了解耦，而实际上提供方接口进行修改，调用方却没有进行修改的时候，会造成异常，所以我们抽取出来。还有就是对内暴露的接口，是很多地方都公用的，所以我们还将接口抽取了出了一个模块，方便引用。可以看到`talent-api`这个模块下是所有对内`feign`接口的信息。







### 前端

### 后台模块
TODO: 
```text
talent
├─talent-api -- 内网接口
│  ├─talent-api-auth  -- 授权对内接口
│  ├─talent-api-biz  -- biz对内接口(文件)
│  ├─talent-api-admin  -- admin后台管理内部接口
│  ├─talent-api-community  -- 社区对内接口
│  ├─ttalent-api-universe  -- 宇宙对内接口
│  ├─ttalent-api-order  -- 订单对内接口
│  ├─ttalent-api-rbac  -- 用户角色权限对内接口
│  ├─ttalent-api-user  -- 用户对内接口
│  └─talent-api-leaf  -- 美团分布式id生成对内接口
├─talent-auth  -- 授权校验模块
├─talent-biz  -- talent 业务代码。如图片上传/短信/email等
├─talent-common -- 一些公共的方法
│  ├─talent-common-cache  -- 缓存相关公共代码
│  ├─talent-common-core  -- 公共模块核心（公共中的公共代码）
│  ├─talent-common-database  -- 数据库连接相关公共代码
│  ├─talent-common-order  -- 订单相关公共类
│  ├─talent-common-rocketmq  -- rocketmq相关公共代码
│  └─talent-common-security  -- 安全相关公共代码
├─talent-gateway  -- 网关
├─talent-admin  -- 后台管理
├─talent-user  -- 用户服务
├─talent-leaf  -- 美团分布式id生成接口
├─talent-payment  -- 支付相关接口
├─talent-rbac  -- 用户角色权限对内接口
├─talent-universe  -- 宇宙
└─talent-community  -- 社区

```





### 技术选型与环境

|        service        |  version  | rose |
| :------------------: | :--------: |   :---:|
| mysql | 5.7.36 |关系型数据库|
| redis | 4.x | 非关系型数据库/分布式缓存 |
| nacos | 2.x | 服务注册与发现 |
| seata | 2.x | 分布式事务 |
| RockMQ | 2.3.x | 消息队列 |
| XXL-JOB |  | 调度服务 |
| Canal |  | 数据同步 |
| Vue |  | JS框架 |
| Gateway |  | 网关 |
| Feign |  | 服务调用 |
| Elasticsearch |  | 数据搜索 |
| Minio |  | 文件上传 |
| Knife4j |  | 整合swagger文档 |
| Element UI |  | UI框架 |



###系统模型

![后端业务扭转与组件模型](..%2Fimage%2FdesignDocumentImage%2Fmodel2.jpg)


## 商城部署后 API 地址
**TODO**

|              服务              |          地址           |
|:----------------------------:|:---------------------:|
|      talent-gatway 网关服务      | http://127.0.0.1:8000 |
|     talent-auth  授权校验服务      | http://127.0.0.1:9101 |
| talent-biz 业务代码服务（如图片上传/短信等） | http://127.0.0.1:9000 |
| talent-leaf 基于美团leaf的生成id服务  | http://127.0.0.1:9100 |
|      talent-order 订单服务       | http://127.0.0.1:9106 |
|     talent-payment 支付服务      | http://127.0.0.1:9113 |
|      talent-rbac 用户角色服务      | http://127.0.0.1:9102 |
|      talent-search 搜索服务      | http://127.0.0.1:9108 |
|       talent-user 用户服务       | http://127.0.0.1:9105 |
|      talent-universe 宇宙服务      | http://127.0.0.1:9122 |
|    talent-community 社区服务     | http://127.0.0.1:9121 |
|                              |                       |





