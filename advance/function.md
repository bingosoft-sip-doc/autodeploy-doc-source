`SipRS`引擎提供对于复杂json结构体的参数求解功能，自动化部署服务扩展了一个函数解析。

### Fn::GetAppEnv

从一个json结构体中，取某一个参数

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
* 参数1：envId

如上所示，为取出env:222222的所有环境参数。

> 环境参数可以在环境的详情页面看到。

![img](..\image\envparam.png)