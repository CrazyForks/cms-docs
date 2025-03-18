# 常见问题

> [!IMPORTANT]
> 首先确定自己是不是最新版，不是就升级到最新版，然后看看问题是否已解决 


## 启动失败

### 示例1：
```bash
RuntimeError: this license key is expired (1:11086)
```

**版本过期了，升级到最新版即可**


### 示例2：

```bash
INFO:     2025-03-03 22:26:05,135 - main      :  54 ➜ 开始校验捐赠码....
ERROR:    2025-03-03 22:26:05,142 - mhttp     : 156 ➜ HTTP请求失败: 连接错误
ERROR:    2025-03-03 22:26:05,146 - mhttp     : 156 ➜ HTTP请求失败: 连接错误
INFO:     2025-03-03 22:26:05,147 - main      :  56 ➜ 校验捐赠码结束....
```

**你的docker连不上cms的授权服务器，可以给docker加上代理启动，如下所示加上这些变量后启动**

```yaml
- HTTP_PROXY=http://192.168.2.118:7890
- HTTPS_PROXY=http://192.168.2.118:7890
- NO_PROXY=localhost,127.0.0.0/8,10.0.0.0/8,172.0.0.0/8,192.168.0.0/16
```

## 9096打不开

**你填的emby地址不可用，换个能用的**

## 快速同步失败

### 目录不存在或已转移：

去网页版115里校验下空间，然后重试

## 自动整理报错

### 示例1：

![自动整理报错](/faq/auto-error.jpg)

**你的重命名规则错了，要用 < > 包裹变量，请参考 [重命名规则](https://github.com/guyue2005/CMSHelp/wiki/5.%E4%B8%8A%E4%BC%A0%E4%B8%8E%E6%95%B4%E7%90%86#%E9%87%8D%E5%91%BD%E5%90%8D%E8%A7%84%E5%88%99)**

改完之后浏览器访问下下面的地址，清下缓存

```bash
http://127.0.0.1:9527/api/config/clear?token=cloud_media_sync&table=rename_log
```


## 字幕未整理

### 原因1：

**字幕文件命名错误，类似于下面的字幕命名才会被整理**

```bash
钢铁侠.2008.2160p.UHD.BluRay.x265.10bit.HDR.TrueHD.7.1-TnT.mkv
钢铁侠.2008.2160p.UHD.BluRay.x265.10bit.HDR.TrueHD.7.1-TnT.srt
钢铁侠.2008.2160p.UHD.BluRay.x265.10bit.HDR.TrueHD.7.1-TnT.chs.srt
钢铁侠.2008.2160p.UHD.BluRay.x265.10bit.HDR.TrueHD.7.1-TnT-chs.srt
```

### 原因2：

**命名规则有问题** 你的重命名规则错了，可能为空的变量要用 < > 包裹

```bash
{title}.{year}.{resource_pix} 错误
{title}.{year}<.{resource_pix}> 正确
```

请参考 [重命名规则](https://github.com/guyue2005/CMSHelp/wiki/5.%E4%B8%8A%E4%BC%A0%E4%B8%8E%E6%95%B4%E7%90%86#%E9%87%8D%E5%91%BD%E5%90%8D%E8%A7%84%E5%88%99)


## 错误码

### 403

**115禁止香港IP访问，请更换VPS**

### 405

**触发风控了，等待解封（一般第一次触发，换个设备扫码就行；触发了多次时间就不一定了）**

### 443

**代理问题，请检查http代理是否正常**


