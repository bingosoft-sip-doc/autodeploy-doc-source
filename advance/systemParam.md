#### EnvParams:ServiceId

> 在服务的申请页面获取当前服务ID

使用场景举例：
云区域获取serviceId，以便判断每个服务的发布区域
```
"Bingo::Cloud::Region": {
    "name": "云区域",
    "params": {},
    "outputs": {
      "text": "regionName",
      "value": "regionId"
    },
    "params": {
      "serviceId": "EnvParams:ServiceId"
    }
  }
```