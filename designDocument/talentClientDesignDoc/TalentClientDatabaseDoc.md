

# 数据库详细设计

数据库列表
完成的用“<input type="checkbox" checked>”标记

## talent_auth
| tableName | description | Check |
| :-------- |-------------| ----- |
|    auth_account       | 统一账户信息表     | ✅ |



### auth_account
统一账户表(平台所有账户信息)

| columnName |  type  | length | 小数点 | not null | 虚拟 | key | describe | default | 自动递增 | 无符号 | 填充零 |
|:-----------|:------|:------|:---|:--------|:--|:---|:--------|:--------|:----|:---|:---|
|  uid  | bigint |   20   |  ❌  |    ✅     | ❌  |  ✅  |   全平台唯一id   |         |  ❌   |  ❌  |  ❌  |
|    username    | varcher |  30  |  ❌  |    ✅    | ❌  |  ❌  | 用户名 |         |  ❌   |  ❌  |  ❌  |
| password | varchar | 64 | ❌ | ✅ | ❌ | ❌ | 密码 |         | ❌ | ❌ | ❌ |
| create_ip | varchar | 15 | ❌ | ✅ | ❌ | ❌ | 创建ip |         | ❌ | ❌ | ❌ |
| sys_type | tinyint | 4 | ❌ | ✅ | ❌ | ❌ | 用户类型见SysTypeEnum 0.普通用户系统 1.商家端 2平台端 |         | ❌ | ❌ | ❌ |
| user_id | bigint | 20 | ❌ | ✅ | ❌ | ❌ | 用户id |         | ❌ | ❌ | ❌ |
| is_admin | tinyint | 4 | ❌ | ❌ | ❌ | ❌ | 是否是管理员 |         | ❌ | ❌ | ❌ |
|   status   |  tinyint  |   4   | ❌ | ✅ | ❌ | ❌ | 状态 1:启用 0:禁用 -1:删除 |  | ❌ | ❌ | ❌ |
| create_time | datetime |        | ❌ | ✅ | ❌ | ❌ | 创建时间 | 根据当前时间戳更新 | ❌ | ❌ | ❌ |
| update_time | datetime |  | ❌ | ✅ | ❌ | ❌ | 更新时间 | 根据当前时间戳更新 | ❌ | ❌ | ❌ |


## **talent_user**
- user 平台用户表, 平台用户注册的时候, 会将平台用户的信息统一存储到talentauth库中的auth_account统一账户信息表
- 同理, A端在新增账户的时候也会将用户信息统一保存到auth_account统一账户信息表

| tableName            | description                                                  | check |
| :------------------- | :----------------------------------------------------------- | :---: |
| user                 | 平台用户表(用户的注册信息记录表)                             |   ✅   |
| user_addr            | 平台用户地址表 1 v n                                         |   ✅   |
| user_account         | 平台用户账户信息表 1 v n                                     |   ✅   |
| user_account_journal | 平台用户账户流水记录表 1 v n                                 |   ✅   |
| user_follow          | 平台用户关注列表 1 v n                                       |   ✅   |
| user_browse_history  | 平台用户浏览历史表 1 v n                                     |   ✅   |
| ~~user_data_board~~  | 平台用户数据看板表 1 v n (数据看板为阶段性统计总数据, 并非实时数据) |       |

## **talent_universe**

| tableName                         | description                  | check |
|:----------------------------------|:-----------------------------|:-----:|
| universe                            | 宇宙表                          |   ✅   |
| universe_article                    | 宇宙内容表 1 v n                  |   ✅   |
| universe_groups       | 宇宙群组表 1 v n                  | ✅ |
| universe_gambit                     | 宇宙话题 1 v n                   |       |
| universe_article_comments | 宇宙内容评论父子表 1 v n      | ✅ |
| universe_article_gifts | 宇宙文章礼物记录表 | ✅ |
| ~~universe_article_comment_like~~   | 宇宙内容评论点赞表 1 v n (考虑做成缓存)     |       |
| ~~universe_user~~                   | 宇宙成员表 1 v n                  |       |
| ~~universe_article_tag~~            | 宇宙内容标签表 1 v n                |       |
| ~~universe_article_data_view~~      | 宇宙内容数据视图表(实时) 1 v n (考虑做成缓存) |       |
| ~~universe_red_packet~~             | 宇宙红包表 1 v 1                  |       |
| ~~universe_red_packet_get_records~~ | 宇宙红包领取记录表 1 v n              |       |
| ~~universe_group~~                  | 宇宙关联的群组(私域业务)                |       |
|  |  | |

- tips:
    - 宇宙内容表: 设置内容属性(官方内容/通告内容等), 社区规则看todo

## talent_biz

| tableName     | description    | check |
| :------------ | :------------- | :---- |
| email_records | 邮件发送记录表 | ✅     |
| dictionaries  | 字典枚举细分表 | ✅     |
|               |                |       |



## talent-payment

| tableName           | description              | check |
| :------------------ | :----------------------- | :---- |
| pay_info            | 订单支付记录(重新设计的) | ✅     |
| pay_recharge_levels | 支付充值档位表           | ✅     |
| pay_universe_gifts  | 支付宇宙礼物表           | ✅     |



## **talent_job**

| tableName      | description   |check|
|:---------------|:--------------|:---:|
| job_universe     | 宇宙工作 1 v n    ||
| job_apply_user | 宇宙工作申请表 1 v n ||


## **talent_advertising** `low`

| tableName             | description               | check |
|:----------------------|:--------------------------|:-----:|
| advertising           | 广告表                       |       |
| advertising_data_view | 广告数据表 1 v 1(实时, 但是考虑做成缓存) |       |

