# 支持Canvas的Leaflet.Path.DashFlow动态流向线


## 简介：

通过对leaflet以及其插件的学习，我们了解到使用`Leaflet.Path.DashFlow`插件可实现轨迹动态展示、管道流向动态展示、河流流向动态展示等，达到增强可视化展示的效果。

但是在使用的过程中，发现该插件有个弊端，就是当初始化地图`preferCanvas`参数为`true`时，及使用`Canvas`方式绘制时，动态效果不可用。

通过对`Leaflet.Path.DashFlow`以及`leaflet`源码的研究，发现动态线的效果主要通过动态刷新`dashOffset`参数的值，以改变线的样式来实现。`L.SVG`在`_updateStyle`的时候，更新了`dashOffset`参数，但是`L.Canvas`在`_updateStyle`时，并没有更新`dashOffset`属性。

由此，我们找到了解决思路，及在`L.Canvas`的`_updateStyle`方法中，参考`L.SVG`的处理方式，添加对`dashOffset`参数的控制。

为方便使用，我们将`L.Path.DashFlow`插件重新封装，大家引用这个插件，即可在`Canvas`和`SVG`两种方式下使用此插件。

## 用法：

该插件使用方式非常简单，只需在正常添加线的时候，加入`dashArray`和`dashSpeed`参数即可。

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

