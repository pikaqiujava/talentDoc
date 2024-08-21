# 接口控制器
[UniverseArticleCommentsController](..%2F..%2F..%2F..%2Ftalent-universe%2Fsrc%2Fmain%2Fjava%2Fcom%2Ftalent%2Fcrows%2Funiverse%2Fcontroller%2Fapp%2FUniverseArticleCommentsController.java)

# /a/universe/article/page

宇宙文章分页接口:
- 入参: userId, 按时间/按热度, 标签, 城市, 类型
- 实现:
    - 场景: 1. 用户的文章列表, 2. 推荐页面的文章列表
    - 用户文章分页列表
      - UserId和条件去es分页查询缓存的用户文章列表
      - 根据时间或者热度(权重)去排序 
    - 返回[EsPageVO](..%2F..%2F..%2F..%2Ftalent-api%2Ftalent-api-search%2Fsrc%2Fmain%2Fjava%2Fcom%2Ftalent%2Fcrows%2Fapi%2Fsearch%2Fvo%2FEsPageVO.java)<[UniverseArticleVO](..%2F..%2F..%2F..%2Ftalent-universe%2Fsrc%2Fmain%2Fjava%2Fcom%2Ftalent%2Fcrows%2Funiverse%2Fvo%2FUniverseArticleVO.java)>对象


# /a/universe/article/detail

宇宙文章详情接口:
- 入参: articleId
- 实现: 
  - es查询文章详细信息
  - 给符合条件的结果递增权重
  - 返回[UniverseArticleVO](..%2F..%2F..%2F..%2Ftalent-universe%2Fsrc%2Fmain%2Fjava%2Fcom%2Ftalent%2Fcrows%2Funiverse%2Fvo%2FUniverseArticleVO.java)对象


todo: 待细化 -> 普通新增(草稿)/发布, 区分业务接口, 单一职责
# /a/universe/article/insert

发布文章页面接口: 
- 入参: 文章详情, 文章状态: 发布还是草稿
- 实现: 
  - 发布的话要设置权重, 设置发布时间
  - 插入es建立索引
  - 返回 Boolean