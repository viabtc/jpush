极光推送Golang客户端
===
### 注意！！！viawallet专用
用于viawallet 2.5.0版本升级后，将当前设备的当前钱包ID关联的设备给踢下线（如果还有老版本的设备，重新进入后还会再次注册，不影响）。防止升级后，apns/极光2个渠道的推送都推过来

目前支持

* Push API v3
* Schedule API v3
* Device API v3
>  base url 修改为device，其他的api将404 https://device.jpush.cn


### 安装

    go get github.com/levigross/grequests
    go get github.com/zwczou/jpush

### 使用

1. 初始化客户端

```go
    client := jpush.NewJpushClient("key", "secret")
```

2. 获取推送唯一标识符 cid

```go
    cidList, err = client.PushCid(1, "push")
```

3. 推送消息

```go
    payload := &jpush.Payload{
        Platform: jpush.NewPlatform().All(),
        Audience: jpush.NewAudience().All().SetTag("abc", "ef").SetTagAnd("filmtest"),
        Notification: &jpush.Notification{
            Alert: "test",
        },
        Options: &jpush.Options{
             TimeLive:       60,
             ApnsProduction: false,
        },
    }
    msgId, err = client.Push(payload)
    // msgId, err = client.PushValidate(payload)
```


4. 创建计划任务

```
    client.ScheduleCreate
```
