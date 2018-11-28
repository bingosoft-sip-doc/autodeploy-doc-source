> SIP::EC2::ElasticIp，创建弹性IP，并绑定到实例

参数：

| 名称              | 显示名称 | 描述                            |
| --------------- | ---- | ----------------------------- |
| desiredAddress  | 指定IP | 为空则不指定                        |
| share           | 是否共享 | 默认不共享                         |
| elasticSubnetId | 出口子网 | 为空则自动指定，但是如果VPC类型为手工选择子网，此项必填 |
| regionId        | 区域   |                               |
| bandwidth       | 带宽   | 默认为1M，类型为数字，单位为M              |
| instanceId      | 实例ID | 为空则不绑定                        |
| line            | 线路   | 默认为default线路                  |

输出信息：

| 名称          | 显示名称    |
| ----------- | ------- |
| address     | IP地址    |
| elasticIpId | 弹性IP的ID |

使用说明：

在模型编辑中，拖动一个弹性IP即可

![img](..\image\EIP.png)

如果不绑定实例，则不需要填写实例ID。

出口子网可以由参数模板中配置。

参数模板：

在网络后面，添加以下参数即可。

```
{
    "Key": "elasticIpSelect",
    "Type": "Bingo::EC2::ElasticIp::Id",
    "DisplayName": "弹性IP",
    "Fn::Source": {
      "regionId": "Ref:regionId",
      "vpcCode": "Ref:vpcId"
    },
    "NoEcho": "FALSE",
    "AllowedCustomization": "TRUE"
  }
```

key必须为`elasticIpSelect`,建议设置为不允许用户修改，此参数依赖区域和用户选择的VPC。

1. 如果用户选择的VPC是外部网络，则参数渲染页面不需要选择弹性IP，流程也不会创建弹性IP
2. 如果用户选择的VPC是内部网络，且自动选择子网，则参数渲染页面不需要选择弹性IP，流程自动创建弹性IP
3. 如果用户选择的VPC是内部网络，且手工选择子网，则参数渲染页面需要用户选择出口网络，流程根据出口网络创建弹性IP

