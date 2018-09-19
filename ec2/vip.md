在SDN网络中，虚拟IP需要从SDN控制器获取，不可以单独使用一个私有IP地址，作为虚拟IP。

### VIP交付

> SIP::EC2::Vip，申请一个VIP

![img](..\image\vip-param.png)

输出信息：

| 名称    | 显示名称   |
| ----- | ------ |
| vipId | vip的ID |

### VIP关联实例

> SIP::EC2::Vip::Associate，将一个VIP，关联到一台云主机

| 名称           | 显示名称    |
| ------------ | ------- |
| vipId        | 虚拟IP的ID |
| instanceCode | 实例编号    |

