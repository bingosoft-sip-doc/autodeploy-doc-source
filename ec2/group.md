> SIP::EC2::SecurityGroup，创建安全组，或者对已有安全组进行授权

参数：

| 名称                | 显示名称  |           |
| ----------------- | ----- | --------- |
| regionId          | 区域    |           |
| securityGroupName | 安全组名称 |           |
| portInfo          | 端口信息  | 分为udp和tcp |

![img](..\image\tcp.png)

如图所示，设置为开放tcp协议，端口信息从参数port中获取。

端口的开放规则支持批量设置，如`22,80,22-33`