自定义指令服务，支持用户对机器下发自定义指令。具体参数如下

| 名称              | 显示名称    | 描述                           |
| --------------- | ------- | ---------------------------- |
| machineId       | 实例的ID   | 指定虚拟机的ID                     |
| name            | 指令名称    |                              |
| command         | 指令内容    |                              |
| desc            | 指令描述    |                              |
| rollbackCommand | 回滚指令内容  | 如果指令运行失败，可以运行回滚指令进行撤销。       |
| taskId          | 部署任务的ID | 如果配置了部署任务ID，生成的指令会归入同一个部署任务。 |

自定义指令，会通过指令下发的方式启动，在部署任务列表中，产生一条指令下发记录。您可以在部署任务和流程实例的详情页面查看到其运行日志和结果。