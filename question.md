### 常见问题

#### 部署任务创建成功，但是不执行

问题描述： 部署任务已经正常创建，但是部署步骤一直未运行，例如下载文件或者挂载存储卷的脚本一直未运行

排障步骤：

1. 检查是否安装部署agent，并且agent已运行

   2.0.0.0以后的agent安装目录同ec2

   1. windows在`C:\Program Files\Bingosoft\DeployAgent`,检查服务中BingosoftDeployAgent的运行状态
   2. linux在`/usr/local/deploy-agent`，运行`ps -ef| grep agent`,查看是否存在`/usr/local/deploy-agent`的进程

2. ​检查agent的网络连接