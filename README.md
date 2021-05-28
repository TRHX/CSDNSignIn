# CSDN Sign In - CSDN 自动签到抽奖

- 语言：Python
- 功能：签到、抽奖（可选）
- 自动签到：GitHub Actions 每天 24 点
- 签到结果通知：Server 酱（可选）、企业微信（可选）、钉钉（可选）
- CSDN 文章链接：https://itrhx.blog.csdn.net/article/details/117375471

# 使用方法

点击右上角【Fork】代码到你的账户，然后点击【Settings】—【Secret】—【New repository secret】，依次填入以下 Name 以及对应的 Value：

---

<font color=#FF0000>**注意：cookie 的值需要你登录后 F12 查看复制过来，cookie 的有效期是多久暂时不得而知，等下次失效了我再回来告诉你们有效期是多久，如果我没说，那就代表一直没失效！😁**</font>

---

|  Name  |  是否为必填项  | 含义  | Value 示例 |
|  -------   |   --------  |   --------  |   --------  |
| CSDN_ID |                <font color=#FF0000>**是**</font>  |  CSDN 的 ID  |   qq_36759224 |
| COOKIE |                 <font color=#FF0000>**是**</font>  |  已登录的 cookie   |  uuid_tt_dd=10_287647...... |
| IF_LUCK_DRAW|    否  |  是否开启抽奖   |    on  |
|  IF_SEVER|             否  |  是否开启 server 酱通知   |    on  |
|  IF_WECHAT|          否  |  是否开启企业微信通知   |      on  |
|  IF_DING  |              否  |  是否开启钉钉通知  |     on  |
|  SEVER_SCKEY  |  取决于 IF_SEVER    |  server 酱的 SCKEY  |  SCU165692T......|
|  WECHAT_URL  |    取决于 IF_WECHAT  |  企业微信机器人地址  |  https://qyapi.weixin.qq.com/cgi-bin/webhook/......  |
|  DING_URL  |          取决于 IF_DING        |  钉钉机器人地址  |  https://oapi.dingtalk.com/robot/send......  |
|  DING_SECRET  |  取决于 IF_DING        |  钉钉机器人加签 SECRET   |  SEC1cb948ba......  |

举例：我需要开启抽奖和 server 酱通知，则需要填的有：

|  Name  |  Value  |
|  -------   |   --------  |
| CSDN_ID |  qq_36759224 |
| COOKIE |  uuid_tt_dd=10_287647...... |
| IF_LUCK_DRAW | on |
|  IF_SEVER  |  on  |
|  SEVER_SCKEY  |  SCU165692T......|

# 演示操作流程

![](https://img-blog.csdnimg.cn/20210529011927743.png)

![](https://img-blog.csdnimg.cn/20210529012512140.png)

![](https://img-blog.csdnimg.cn/20210529025050577.png)

# 更改签到时间

如果你需要更改每天签到的时间，则需要更改 `.github/workflows/csdn-sign-in.yml` 文件里面 `cron: 0 16 * * *` 的值，这里使用的是 Linux crontab 定时任务命令，`0 16 * * *` 表示每天凌晨运行一次，注意这里使用的是 UTC 国际标准时间，与北京时间相差 8 个小时，所以 UTC 时间 16 点也就是北京时间的 24 点。
