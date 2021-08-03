# CSDN Sign In - CSDN 自动签到抽奖

- 语言：Python
- 功能：签到、抽奖（可选）
- 自动签到：GitHub Actions 每天 24 点
- 签到结果通知：Server 酱（可选）、企业微信（可选）、钉钉（可选）
- CSDN 文章链接：https://itrhx.blog.csdn.net/article/details/117375471
- 更多爬虫项目：https://github.com/TRHX/Python3-Spider-Practice

# 注意事项

- **cookie 的值需要你登录后 F12 查看复制过来，~~cookie 的有效期是多久暂时不得而知，等下次失效了我再回来告诉你们有效期是多久，如果我没说，那就代表一直没失效！😁~~**

- **经过测试，cookie 的有效期在 45 天左右，失效后需要重新复制一个新 cookie 过来！**

- **如果你开启了自动抽奖，程序会识别你当前还有多少次抽奖次数，如果抽奖次数为0，则仍然不执行抽奖任务！**

- **是否开启抽奖、消息通知，如果需要开启则填 on，不填或者填其他任何值则视为不开启！**

# 使用方法

点击右上角【Fork】代码到你的账户，然后点击【Settings】—【Secret】—【New repository secret】，依次填入以下 Name 以及对应的 Value：

|  Name  |  是否为必填项  | 含义  | Value 示例 |
|  -------   |   --------  |   --------  |   --------  |
| **CSDN_ID** |   **是**  |  **CSDN 的 ID**  |   **qq_36759224** |
| **COOKIE** |    **是**  |  **已登录的 cookie**   |  **uuid_tt_dd=10_287647......** |
| IF_LUCK_DRAW|    否  |  是否开启抽奖   |    on  |
|  IF_SEVER|             否  |  是否开启 server 酱通知   |    on  |
|  IF_WECHAT|          否  |  是否开启企业微信通知   |      on  |
|  IF_DING  |              否  |  是否开启钉钉通知  |     on  |
|  SEVER_SCKEY  |  取决于 IF_SEVER    |  server 酱的 SCKEY  |  SCU165692T......|
|  WECHAT_URL  |    取决于 IF_WECHAT  |  企业微信机器人地址  |  https://qyapi.weixin.qq.com/cgi-bin/webhook/......  |
|  DING_URL  |          取决于 IF_DING        |  钉钉机器人地址  |  https://oapi.dingtalk.com/robot/send......  |
|  DING_SECRET  |  取决于 IF_DING        |  钉钉机器人加签 SECRET   |  SEC1cb948ba......  |

举例：如果需要开启抽奖和 server 酱通知，则需要填的有：

|  Name  |  Value  |
|  -------   |   --------  |
| CSDN_ID |  qq_36759224（你的 CSDN ID） |
| COOKIE |  uuid_tt_dd=10_287647...... (复制过来的你的 cookie) |
| IF_LUCK_DRAW | on |
|  IF_SEVER  |  on  |
|  SEVER_SCKEY  |  SCU165692T...... （你的 server 酱 SCKEY）|

# 演示操作流程

![](https://img-blog.csdnimg.cn/20210529011927743.png)
![](https://img-blog.csdnimg.cn/20210529012512140.png)
![](https://img-blog.csdnimg.cn/20210529025050577.png)

# 消息通知

## Server 酱

Server 酱首页：sc.ftqq.com

什么是 Server 酱？简单来说，登录 Server 酱后，会分配给你一个 SCKEY，通过向专门的 URL 发送 get 或者 post 请求，你的微信就会收到对应的消息，对于不使用企业微信和钉钉的用户来说，这种方法是最方便的。目前有标准版和 Turbo 版，据说标准版会下线，目前还能使用，所以暂时使用的是标准版。若被弃用，我会第一时间更新。实现效果：

![](https://img-blog.csdnimg.cn/20210530032641883.png)

## 企业微信

如果你是一个企业微信群的群主，那么可以在群名右键添加一个机器人，添加成功后会给你一个机器人的 URL 地址，向这个 URL 发送 post 请求就可以在群里看到对应的消息，支持 markdown、text、图片等多种格式，具体可以查看机器人配置说明。

![](https://img-blog.csdnimg.cn/20210528234109149.png)
![](https://img-blog.csdnimg.cn/20210528234109439.png)
![](https://img-blog.csdnimg.cn/2021053003272343.png)

## 钉钉

和企业微信类似，如果你是一个钉钉群的群主，依次右键【群设置】—【群智能助手】—【添加机器人】，选择自定义（通过webhook接入自定义访问）机器人，安全设置里面选择【加签】，添加完成后你会得到一个机器人的 Webhook URL 和一个加签的密钥，之后使用特定的算法将一些参数和 URL 组成新的 URL，再向这个 URL 发送 post 请求就可以在群里收到消息了，具体使用方法参见官方文档：https://developers.dingtalk.com/document/app/custom-robot-access

![](https://img-blog.csdnimg.cn/20210528234901161.png)
![](https://img-blog.csdnimg.cn/20210528234901448.png)
![](https://img-blog.csdnimg.cn/20210528235219447.png)
![](https://img-blog.csdnimg.cn/20210530032751582.png)


# 更改签到时间

如果你需要更改每天签到的时间，则需要更改 `.github/workflows/csdn-sign-in.yml` 文件里面 `cron: 0 16 * * *` 的值，这里使用的是 Linux crontab 定时任务命令，`0 16 * * *` 表示每天凌晨运行一次，注意这里使用的是 UTC 国际标准时间，与北京时间相差 8 个小时，所以 UTC 时间 16 点也就是北京时间的 24 点。
