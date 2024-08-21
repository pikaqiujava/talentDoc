# 优秀的Elasticsearch托管操作工程


## easy-es Elasticsearch操作简化工具

[easy-es](https://gitee.com/dromara/easy-es)

- 将其拆解, 装载进`talent-search`模块
- 将所有方式抽离, 通过feign调用实现具体功能, 用于支撑搜索/权重等业务的中台服务
- 解藕化`talent-search`, 让其可以随时独立成一个中台

