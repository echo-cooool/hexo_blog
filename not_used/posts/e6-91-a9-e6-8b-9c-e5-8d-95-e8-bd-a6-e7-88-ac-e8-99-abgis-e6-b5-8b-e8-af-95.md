---
title: 摩拜单车爬虫+GIS测试
tags:
  - Good
  - 爬虫
url: 77.html
id: 77
categories:
  - Python
date: 2018-04-13 22:47:01
---

这次源于一次偶然的抓包，在手机上使用packet capture 对微信小程序抓包，偶然发现了如下的数据：

    {
      "code": 0,
      "message": "",
      "biketype": 0,
      "autoZoom": true,
      "radius": 150,
      "object": [
        {
          "distId": "8630779582",
          "distX": 116.28002632187257,
          "distY": 39.91022600618757,
          "distNum": 1,
          "distance": "62",
          "bikeIds": "8630779582#",
          "biketype": 1,
          "type": 0
        },
        {
          "distId": "8630367786",
          "distX": 116.27939881379473,
          "distY": 39.91056046398812,
          "distNum": 1,
          "distance": "117",
          "bikeIds": "8630367786#",
          "biketype": 1,
          "type": 0
        },
        {
          "distId": "0106005017",
          "distX": 116.27949896034224,
          "distY": 39.91104357270857,
          "distNum": 1,
          "distance": "131",
          "bikeIds": "0106005017#",
          "biketype": 2,
          "type": 0
          }
    
    

那自然是高兴地不得了，标准的JSON So Eazy ！！ 借鉴之前爬学而思的程序【上次爬了一大堆资料，嘿嘿嘿】 将API地址和请求内容分成两个变量，将其中的经纬度信息分割出来，分别各使用一个变量，再对其进行拼接即可。

    #获取数据
    def bike(longitude,latitude):
        url = 'https://mwx.mobike.com/mobike-api/rent/nearbyBikesInfo.do'
        #print('请求数据')    
        latitude = str(latitude)
        longitude = str(longitude)
        data="verticalAccuracy=0&latitude="+latitude+"&errMsg=getLocation:ok&accuracy=30&horizontalAccuracy=30&speed=-1&longitude="+longitude+"&citycode=010&wxcode=003GVtgj2jeyBF0cxQgj229Igj2GVtg1"
        result = getHtml(url,data)
        return result
    

之后由于还不会其他的爬虫方法，就使用最简单的`import urllib.request` 代码如下

    def getHtml(url,data):
        user_agent='Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.82 Safari/537.36'
        headers = {
                    'charset':'utf-8',
                    'platform':'4',
                    'referer':'https://servicewechat.com/wx40f112341ae33edb/1/',
                    'content-type':'application/x-www-form-urlencoded',
                    'user-agent':'MicroMessenger/6.5.4.1000 NetType/WIFI Language/zh_CN',
                    'host':'mwx.mobike.com',
                    'connection':'Keep-Alice',
                    'accept-encoding':'gzip',
                    'cache-control':'no-cache'
                }
        #data = urllib.parse.urlencode(values)
        #print(url+'?'+data)
        timeout = 1  
        socket.setdefaulttimeout(timeout)  
        print(url+'?'+data)
        response_result = urllib.request.Request(url+'?'+data)  
        html = urllib.request.urlopen(response_result).read()  
    
        return html
    

`header`也一样是抓包出来的，反正就是copy嘛~~ 最后就是经纬度的范围，没有什么太好的方法。

    划定一个区域
    循环套循环
    

于是就出现了如下的代码

    for longitude in range(1160000,1168000,80):
        longitude = longitude/10000
        for latitude in range(396000,403000,80):       
            latitude = latitude/10000
            #print(longitude)
            #print(latitude)
            getbike(latitude,longitude)
    

之所以要把经纬度扩大10000倍，是因为`range（）`并不接受`float`型步长，所以只能将其变成整形，之后再变回去，，唉。 最后是所需要的库：

    import urllib.parse
    import urllib.request
    import json
    import csv
    import os
    import time
    import socket  
    import urllib.request 
    

代码已经传到Github 地址：https://github.com/w1109790800/Mobike-Reptile

* * *

Gis的分析结果没太大进展，大冬天的谁骑车，，， \[caption id="attachment\_13575" align="alignnone" width="640"\]\[caption id="attachment\_14514" align="alignnone" width="640"\]![也就山上没车](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-85.jpg) 也就山上没车\[/caption\] 也就山上没车\[/caption\] 最后附一部分数据【数据量太大，需要的话去github中下载吧】 \[video width="960" height="480" mp4="https://x.wangyuyang.top/wp-content/uploads/2018/05/342f20c152fb54ac06b2c42f883cbecf.mp4"\]\[/video\] \[caption id="attachment_14515" align="alignnone" width="174"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-86.jpg) \[/caption\] \[caption id="attachment_14516" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-87.jpg) \[/caption\] \[caption id="attachment_14517" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-88.jpg) \[/caption\]

    distId      distX       distY
    106162799   116.0003669 39.60155466
    106741325   116.0027729 39.59998057
    106190593   116.0053821 39.60265709
    106003828   116.0063136 39.59663351
    106162799   116.0003669 39.60155466
    106190593   116.0053821 39.60265709
    106741325   116.0027729 39.59998057
    106029871   116.0005932 39.61392113
    106622939   116.0118808 39.60652963
    106133660   115.9955102 39.61525816
    106003828   116.0063136 39.59663351
    106029871   116.0005932 39.61392113
    106006181   116.0018439 39.6175667
    106029871   116.0005932 39.61392113
    .
    .
    .