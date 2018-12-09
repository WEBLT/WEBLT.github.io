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
首先创建圆形区域；然后定义8个百度坐标点，创建对应的marker，将marker添加在地图中判断marker是否在圆形区域中，若在，点击marker时，弹出信息窗口显示“在圆形区域内”，若不在，则显示“不在圆形区域内”。具体实现如下：

<!DOCTYPE html>
<html>
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
	<meta name="viewport" content="initial-scale=1.0, user-scalable=no" />
	<style type="text/css">
		body, html {width: 100%;height: 100%;margin:0;font-family:"微软雅黑";}
		#allmap{width:100%;height:500px;}
		p{margin-left:5px; font-size:14px;}
	</style>
	<script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=gNA0Loz4iFGwRxSFDy67E1B5Biy4vyfy"></script>
	<script type="text/javascript" src="http://api.map.baidu.com/library/GeoUtils/1.2/src/GeoUtils_min.js"></script>
<title>圆形区域判断</title>
</head>
<body>
	<div id="allmap"></div>
</body>
</html>
<script type="text/javascript">
// 创建Map
var map = new BMap.Map("allmap");    
//创建一个圆
var circle = new BMap.Circle(new BMap.Point(108.966956, 34.231598),1000,{fillColor:"white", strokeWeight: 3 ,fillOpacity: 0.5, strokeOpacity: 0.5});
  var point2s = [  
new BMap.Point(108.9676,34.211),        
       new BMap.Point(108.9665,34.231), 
       new BMap.Point(108.9681,34.233),  
       new BMap.Point(108.9695,34.229),  
       new BMap.Point(108.9731,34.240),  
       new BMap.Point(108.9712,34.250),  
       new BMap.Point(108.9660,34.230),  
       new BMap.Point(108.9676,34.232),
       ];
function addMarker(points){
     for(var i=0, pointsLen = points.length; i<pointsLen; i++) {
          var marker = new BMap.Marker(points[i]);
          map.addOverlay(marker);
          marker.setAnimation(BMAP_ANIMATION_BOUNCE);  //增加点的弹跳动画
     //添加监听事件
         (function() {
              var thePoint = points[i];
              marker.addEventListener("click",
              function() {
              showInfo(this,thePoint);
              });
              })();  
            }
         }
function showInfo(thismarker,point) {
if(BMapLib.GeoUtils.isPointInCircle(point,circle)){
       var infoWindow = new BMap.InfoWindow("在圆形区域内");
       thismarker.openInfoWindow(infoWindow); //图片加载完后重绘infoWindow
       }else
      {
       var infoWindow = new BMap.InfoWindow("不在圆形区域内");
       thismarker.openInfoWindow(infoWindow); //图片加载完后重绘infoWindow
      }
      }
	function initialize() {  
    alert("点击标注点可以显示是否在区域内"); 
map.addControl(new BMap.NavigationControl());               // 添加平移缩放控件  
map.addControl(new BMap.ScaleControl());                    // 添加比例尺控件  
map.addControl(new BMap.OverviewMapControl());              //添加缩略地图控件  
map.enableScrollWheelZoom();                            //启用滚轮放大缩小  
map.addControl(new BMap.MapTypeControl());          //添加地图类型控件  
var point = new BMap.Point(108.966956, 34.231598);    // 创建点坐标  
map.centerAndZoom(point,15);                // 初始化地图,设置中心点坐标和地图级别。  
addMarker(point2s); 
map.addOverlay(circle);
}
initialize();
</script>

# 3、实现代码

![/styles/images/03.png]({{ '/styles/images/03.png' | prepend: site.baseurl  }})
![/styles/images/04.png]({{ '/styles/images/04.png' | prepend: site.baseurl  }})
