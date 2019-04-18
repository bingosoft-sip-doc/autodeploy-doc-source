`SipRS`引擎提供对于复杂json结构体的参数求解功能，自动化部署服务扩展了一个函数解析。

[toc]
### EnvParams:EnvId

对于环境Id，系统提供了获取的函数，方便在运维方案中，通过环境ID查询其他参数信息


```
{
    "Key": "envId",
    "AllowedCustomization": "FALSE",
    "DefaultValue": "EnvParams:EnvId",
    "sort": 2
  }
```

### Fn::GetAppEnv

获取某一个环境的参数信息

```
{“envParam” : 
    {
        "Fn::GetAppEnv": [
            "222222"
        ]
    }
}
等同于
{"envParam" : {
    "user" : "root",
    "password" : "111111"
}}

```
这里也可以引用EnvParams:EnvId参数
```
{“envParam” : 
    {
        "Fn::GetAppEnv": [
            EnvParams:EnvId
        ]
    }
}
```
* 参数1：envId

如上所示，为取出env:222222的所有环境参数。

> 环境参数可以在环境的详情页面看到。

![img](..\image\envparam.png)

除了设计者自定义的环境参数以外，系统还提供了以下几个固定参数：
```
"envId": "bb19e468-0c08-4c52-a91b-2fe4f98b93e5",
"envName": "test222",
"envStatus": "ready",
"createTaskId": "22f6742d-46ba-433c-b0e5-ef99b943012f",
"createProcessInstanceId": "e3cc0a51-4bbe-11e9-9ff8-d00dd670a106",
```

### Fn::GetAtt
从一个json结构中，获取一个参数

```
{
          "Fn::GetAtt": [
            {
              "createProcessInstanceId":"11111111111111111"
            },
            "createProcessInstanceId"
          ]
        }
```
* 参数1：jsonObject
* 参数2：取值的key

如下所示，是用来从环境参数中获取到`createProcessInstanceId`.
```
{
    "Key": "root",
    "Type": "String",
    "DefaultValue": {
      "Fn::GetProcessOutputs": [
        {
          "Fn::GetAtt": [
            {
              "Fn::GetAppEnv": [
                "EnvParams:EnvId"
              ]
            },
            "createProcessInstanceId"
          ]
        },
        "test",
        [
          "user"
        ]
      ]
    },
    "NoEcho": "FALSE",
    "AllowedCustomization": "FALSE",
    "UIGroup": "test",
    "sort": 1
  }
  ```

  ### Fn::GetProcessOutputs
  获取流程的输出信息
```
  {
      "Fn::GetProcessOutputs": [
        "1111111",
        "test",
        [
          "user"
        ]
      ]
    }
```
  * 参数1：流程ID
  * 参数2：流程中的namespace
  * 参数3：namespace中的参数名，可以为多个

如下所示，是用来从流程输出中取到namespace为test的节点下，key为user的值.
```
{
    "Key": "root",
    "Type": "String",
    "DefaultValue": {
      "Fn::GetProcessOutputs": [
        {
          "Fn::GetAtt": [
            {
              "Fn::GetAppEnv": [
                "EnvParams:EnvId"
              ]
            },
            "createProcessInstanceId"
          ]
        },
        "test",
        [
          "user"
        ]
      ]
    },
    "NoEcho": "FALSE",
    "AllowedCustomization": "FALSE",
    "UIGroup": "test",
    "sort": 1
  }
  ```

### Fn::GetProcessParams

获取流程实例的参数

```
{
      "Fn::GetProcessParams": [
        ”111111“,
        "database"
      ]
    }
```
* 参数1：流程ID
* 参数2：参数名/namespace名，如果只有两个参数，则认为是参数名
* 参数3：如果参数为json，则进一步取值

如下所示，是用来从流程输出中取到namespace为test的节点下，key为user的值.
```
如果流程111的参数如下
{
    "username":"zhangshan",
    "slave":{
        "image":"redhat"
    }
}
则取值为：
{
    "Key": "username",
    "Type": "String",
    "DefaultValue": {
      "Fn::GetProcessParams": [
        "111",
        "username"
      ]
    }
  },
  {
    "Key": "image",
    "Type": "String",
    "DefaultValue": {
      "Fn::GetProcessParams": [
        "111",
        "slave",
        ["image"]
      ]
    }
  }
  ```

 ### Fn::MathParse

 > 目前支持在SIP4.2以上的版本中 

进行数学表达式的计算
* 参数1：包括加减乘除，括号等运算在内的数学表达式

```
Fn::MathParse(exp)

Fn::MathParse(3*2)

# 参数引用
Fn::MathParse(${size}*2)
```
