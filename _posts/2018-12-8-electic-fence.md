---
layout: post
title:  调用百度地图API实现电子围栏
date:   2018-12-08 15:51:00 +0800
categories: 作业
tag: 教程
---

* content
{:toc}


# 1、准备工作			

首先在百度地图网站注册百度地图开发者账号，然后创建应用并获取应用的AK值。

![/styles/images/01.png]({{ '/styles/images/01.png' | prepend: site.baseurl  }})


# 2、电子围栏的实现		
首先创建圆形区域；然后定义8个百度坐标点，创建对应的marker，将marker添加在地图中判断marker是否在圆形区域中，若在，点击marker时，弹出信息窗口显示“在圆形区域内”，若不在，则显示“不在圆形区域内”。具体见下图：

![/styles/images/02.png]({{ '/styles/images/02.png' | prepend: site.baseurl  }})

# 3、实现代码
详情见[电子围栏](https://github.com/WEBLT/WEBLT.github.io)
