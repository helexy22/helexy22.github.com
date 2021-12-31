---
layout:     post   				    # 使用的布局（不需要改）
title:    如何使用 Tasker 自动记录每天早餐醒来的天气和位置				# 标题 
subtitle:  将位置和气温添加到 Googe Calendar 中  #副标题
date:       2021-10-31 				# 时间
author:     helexy22 						# 作者
# header-img: img/post-bg-2015.jpg  #这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Tool
    - Android
---

虽然日记工具也具有同样的功能，只是将记录集成到日历中，方便每天查看或非周期性回顾。

## Tasker 获取 GPS 位置

### Get Location v2

> [Get Location v2](https://tasker.joaoapps.com/userguide/en/help/ah_get_current_location.html)
> 
> 注意：由于地理坐标系的偏移，建议使用坐标转换，转换为CN的坐标系，获得更高精度的地理位置编码。

获取经度、纬度变量 `%gl_longitude`、`%gl_latitude`

### 坐标转换
> Web服务 API|高德地图API](https://lbs.amap.com/api/webservice/guide/api/convert) Web API。

将 GPS(WGS-84)转换为高德(GCJ-02)坐标系，使用高德地图 [坐标转换-API文档-开发指南> 

```
https://restapi.amap.com/v3/assistant/coordinate/convert?locations=116.481499,39.990475&coordsys=gps&output=xml&key=<用户的key>
```

使用 HTTP Request 发送请求
![HTTP Request](https://raw.githubusercontent.com/helexy22/images/master/2021/20211231185848.png)

经纬度坐标：`%http_data.locations` 


## 获取经纬度下的天气状况

> 使用彩云天气 API，需要申请 Key
> 
> [天级预报接口/v2.5 - CaiyunWiki](https://open.caiyunapp.com/%E5%A4%A9%E7%BA%A7%E9%A2%84%E6%8A%A5%E6%8E%A5%E5%8F%A3/v2.5)


```
https://api.caiyunapp.com/v2.5/<用户的key>/-74.0060,40.7128/daily.json?lang=en_US
```

彩云天气获取的天气状况为英文，可以使用其他 API 获取。此处还推荐以下 API：

1. [openweathermap](https://openweathermap.org/current#geo)
2. [和风天气-逐天天气预报 - API | 和风天气开发平台](https://dev.qweather.com/docs/api/weather/weather-daily-forecast/)


## 逆地理编码获取详细结构化地址

> 使用高德地图 API，需要申请 Key


[地理/逆地理编码-API文档-开发指南-Web服务 API|高德地图API](https://lbs.amap.com/api/webservice/guide/api/georegeo)

```
https://restapi.amap.com/v3/geocode/regeo?output=xml&location=116.310003,39.991957&key=<用户的key>&radius=100&extensions=all
```

解析得到具体的地址`%http_data.formatted_address`

## 定时添加日历项

增加定时配置文件，添加到 google calendar,此处可以添加 Get Location v2 获得的 GoogleMap URL。

注意 Taker 相关权限的设置，例如后台获取位置、读取日历的、自动启动等权限，设置非电池优化项等。

![](https://raw.githubusercontent.com/helexy22/images/master/2021/20211231191639.png)


## 其他参考

- [[Tasker]2小时降水警告教程](https://mp.weixin.qq.com/s/xyLXCj8IUiM1M5A445V1wA)
- [解析数据 | Tasker配置教程](https://taskerm.com/2021/06/28/structured-variables.html)
- [Tasker+高德 实现位置&轨迹记录，云端存储，链接分享_273.15的文章-CSDN博客](https://blog.csdn.net/h137242126/article/details/90549371)