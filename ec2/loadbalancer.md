负载均衡，申请云平台原生的负载均衡实例。

### 负载均衡交付

> SIP::EC2::LoadBalancer，交付一台负载均衡实例

参数可以在执行器中查看。

输出为：

| 名称             | 显示名称   |
| -------------- | ------ |
| loadBalancerId | 负载均衡ID |

### 负载均衡注册实例

> SIP::EC2::LoadBalancer::Register，将一台云主机，注册到负载均衡集群中

参数：

| 名称             | 显示名称   |
| -------------- | ------ |
| loadBalancerId | 负载均衡ID |
| instanceCode   | 实例编号   |

