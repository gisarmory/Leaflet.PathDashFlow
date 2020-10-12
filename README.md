# Leaflet.PathDashFlow
Leaflet 动态流向线。

## 简介：

使用Leaflet.Path.DashFlow可实现轨迹动态展示、管道流向动态展示、河流流向动态展示等，增强可视化展示效果。

使用此插件的时候，当初始化地图“ preferCanvas”参数为“true”时，及使用“Canvas”方式绘制时，效果不可用，经研究，需要对“leaflet\layer\vector\Canvas.js”中“_updateDashArray”和“_fillStroke”两个方法进行处理，我们将处理后的代码与”L.Path.DashFlow.js“合并封装成Leaflet.PathDashFlow插件，方便大家使用。

## 用法：

使用方式也很简单，只需引入插件在正常添加线、面的时候，加入“ dashSpeed”参数即可。

## 示例：

~~~ html
    <!-- 引入leafletapi -->
    <link rel="stylesheet" href="./lib/leaflet.css" />
    <script src="./lib/leaflet.js"></script>

    <!-- 引入图层组显示隐藏插件 -->
    <script type="text/javascript" src='../dist/Leaflet.PathDashFlow.min.js'></script>
~~~

~~~ js
	// 初始化地图
    var map = L.map('map', {
        center: [39.924317, 116.390619],
        zoom: 14,
        preferCanvas: true // 使用canvas模式渲染矢量图形 
    });
    // 添加底图
    var tiles = L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png').addTo(map);

    var latlngs = [ [39.898457, 116.391844], [39.898595, 116.377947], [39.898341, 116.368001], [39.898063, 116.357144], [39.899095, 116.351934], [39.905871, 116.350670], [39.922329, 116.349800], [39.931017, 116.349671], [39.939104, 116.349225], [39.942233, 116.349910], [39.947263, 116.366892], [39.947568, 116.387537], [39.947764, 116.401988], [39.947929, 116.410824], [39.947558, 116.426740], [39.939700, 116.427338], [39.932404, 116.427919], [39.923109, 116.428377], [39.907094, 116.429583], [39.906858, 116.414040], [39.906622, 116.405321], [39.906324, 116.394954], [39.906308, 116.391264], [39.916611, 116.390748] ];

    //添加动态线
    var path = L.polyline(latlngs, {
        weight: 5,
        dashArray: '15,15',
        dashSpeed: -30
    }).addTo(map);
~~~

下面是在线示例：

[在线示例](http://gisarmory.xyz/Leaflet.PathDashFlow/examples/index.html)



## 君子协议
只要star本库，并关注公众号“GIS兵器库”，你就可以免费使用此插件。公众号二维码：

![](http://blogimage.gisarmory.xyz/20200923063756.png)

（若上方二维码无法显示，点此链接 [GIS兵器库](http://blogimage.gisarmory.xyz/20200923063756.png) ）

## 相关链接

[Leaflet](https://leafletjs.com/index.html)、[Leaflet.Path.DashFlow](https://gitlab.com/IvanSanchez/Leaflet.Path.DashFlow)

## 免责声明

该插件中集成的纠偏算法，是基于网络上公开已知的，其他语言算法实现的移植版本，作者不对其准确性和合法性做保证。**请在遵守国家保密法的前提下自行斟酌使用**。