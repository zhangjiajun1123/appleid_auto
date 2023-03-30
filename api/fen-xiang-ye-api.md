# 分享页API

简短备注支持通过分享页面链接，以JSON方式获取账号信息，用于对接其他APP

分享页面链接指页面的代码，并非整个URL

API地址：`/shareapi/<link>/[password]`\
请求方法：`GET`\


### 输入参数

| 参数       | 值/类型   | 说明                |
| -------- | ------ | ----------------- |
| link     | String | 分享页代码             |
| password | String | 分享页密码（若未设置密码则不需要） |

### 返回参数

| 参数       | 值/类型   | 说明          |
| -------- | ------ | ----------- |
| status   | Bool   | 操作成功/失败     |
| msg      | String | 提示信息        |
| accounts | Array  | 账号列表（格式见下表） |

### 账号信息

| 参数          | 值/类型   | 说明     |
| ----------- | ------ | ------ |
| username    | String | 账号     |
| password    | String | 密码     |
| status      | Bool   | 账号状态   |
| last\_check | String | 上次检查时间 |
| remark      | String | 账号前端备注 |
