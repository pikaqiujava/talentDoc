# 接口控制器
[UserRegisterController](..%2F..%2F..%2F..%2Ftalent-user%2Fsrc%2Fmain%2Fjava%2Fcom%2Ftalent%2Fcrows%2Fuser%2Fcontroller%2Fapp%2FUserRegisterController.java)

# /ua/user/register

app注册接口:
- 入参: 用户提交用户名, 密码, 邮箱验证码为必要参数
- 实现:
  - service层调用`segmentFeignClient.getSegmentId`获取分布式Id作为用户的唯一主键id
  - service层save保存用户信息
  - 调用`accountFeignClient.save`保存到统一用户表, 返回auth_account表主键id
  - controller层调用`accountFeignClient.storeTokenAndGetVo`签发token完成登陆
  - 返回[TokenInfoVO](..%2F..%2F..%2F..%2Ftalent-api%2Ftalent-api-auth%2Fsrc%2Fmain%2Fjava%2Fcom%2Ftalent%2Fcrows%2Fapi%2Fauth%2Fvo%2FTokenInfoVO.java)对象