# Genshin Cloud Game Helper

每天帮你获取 15 分钟云原神时间~

## 配置教程

### 全局配置

```json
// global.json
{
    "sendMail": true,
    "mailConfig": {
        "user":"",
        "pass":"",
        "mailto":"",
        "smtpServer":"",
        "smtpPort":"",
        "smtpSecure":true
    }
}
```

> sendMail   bool, 是否在运行结束后将结果发送至指定邮箱，false 时 mailConfig 中的内容可为空
> mailConfig 配置
> 
> > user 发送方邮箱
> > 
> > pass 有授权码的填授权码，没有的填密码, 使用密码报错就一般填入授权码即可
> > 
> > mailto 目标邮箱
> > 
> > smtpServer 发送邮件时使用的 SMTP 服务器地址
> > 
> > smtpPort SMTP 服务器端口
> > 
> > smtpSecure 如果 SMTP 服务器使用 SSL/TLS，那么为 true，如果使用 STARTTLS 或不使用加密，那么为 false

对于常用的邮件而言，配置列举如下

| 服务    | server       | port    | secure |
|:-----:|:------------:|:-------:|:------:|
| QQ 邮箱 | smtp.qq.com  | 465/587 | true   |
| 网易邮箱  | smtp.163.com | 465     | true   |
| ...   | ...          | ...     | ...    |

其余邮箱服务的配置可以在对应服务商的帮助文档中找到

### 用户配置

先放一个配置模板

```
{
    "token":"",
    "client_type":"",
    "device_name":"",
    "device_model":"",
    "device_id":"",
    "sys_version":"",
    "channel":""
}
```

具体数据 请看“抓包”环节

> token 是在云原神登录后用于验证的标记
> client_type 1 代表 IOS 设备 2 代表 安卓/鸿蒙 设备
> device_name 设备名称
> device_model 设备型号
> device_id 在米哈游服务器中注册的 uuid
> sys_version 系统版本 安卓/鸿蒙 中为系统版本, IOS 设备中为 ios 版本
> channel 下载渠道 IOS 设备填"app store" 安卓&鸿蒙填"mihoyo" (以抓包为准，我也不知道渠道服是不是这个)

### 抓包

> > # IOS
> > 
> > App Store 中下载应用 Stream（用于抓包）
> > 具体看视频
> > 看不了/不显示的, 可以手动访问 https://hzsj.coding.net/p/ayakaturtleshop/d/PublicResource/git/raw/master/c9f1a9b91951b0f1c2da8f3817274074.mp4?download=false
> > <video src="https://hzsj.coding.net/p/ayakaturtleshop/d/PublicResource/git/raw/master/c9f1a9b91951b0f1c2da8f3817274074.mp4?download=false"></video>
> 
> # 安卓&鸿蒙
> 
> > （来自 https://bili33.top/posts/MHYY-AutoCheckin-Manual)
> > 因为云原神是在手机上运行的，所以你需要安装一个手机上的抓包软件（如 HttpCanary，或者如果你能够用 fiddler 电脑运行去抓也行）
> > [![看就完了](https://cdn.bilicdn.tk/gh/Vikutorika/assets@master/img/Github/MHYY-AutoCheckin/HTTPCANARY-Result.jpg?download=false)]
> > 一定要记得装抓包软件提供的证书，要不然解不了 SSL 连接，一定要先登录并成功进去了再启动抓包软件！！！
> > [![看就完了](https://cdn.bilicdn.tk/gh/Vikutorika/assets@master/img/Github/MHYY-AutoCheckin/HTTPS-REQUEST-RESULT.png?download=false)]
> > 这里面只要是个 HTTP 链接，随便一个里面都有我们所需要的东西，这里我就点开了一个链接，在请求里面有所有我们需要的东西，而解释我都写在图片里面了

二者抓到的包差不多，抓到包之后有以下对应关系

```json
{
    "token":"x-rpc-combo_token",
    "client_type":"x-rpc-client_type",
    "device_name":"x-rpc-device_name",
    "device_model":"x-rpc-device_model",
    "device_id":"x-rpc-device_id",
    "sys_version":"x-rpc-sys_version",
    "channel":"x-rpc-channel"
}
```

在 `configs` 文件夹里创建一个 JSON 文件(任意名称)
将抓包得到的配置填进去  
如果想一次性签到多个用户，创建任意名称的 JSON 文件即可，
程序会自动扫描 configs 文件夹下面的文件

## 另外

程序会自动获取最新的云原神版本，确保数据与用户一样
