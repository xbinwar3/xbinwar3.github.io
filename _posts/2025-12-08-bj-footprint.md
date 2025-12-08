---
layout: default
title: "足迹地图"
---
    <style type="text/css">
     #mountainMap {width: 100%; height: 100%; overflow: hidden; margin:0; font-family:"微软雅黑";}
    </style>
    <script type="text/javascript" src="https://api.map.baidu.com/api?v=3.0&ak=zXRSd3RxTMcC36ULo39lCAKPP6uZesER"></script>

    <div id="mountainMap"></div>
    <script type="text/javascript">
        // 初始化地图[3](@ref)
        var map = new BMap.Map("mountainMap");
        
        // 设置初始中心点和缩放级别[3](@ref)
        map.centerAndZoom(new BMap.Point(110.0956, 34.4866), 5);
        map.enableScrollWheelZoom(true); // 启用滚轮缩放[3](@ref)
        
        // 添加地图控件[3](@ref)
        map.addControl(new BMap.NavigationControl());
        map.addControl(new BMap.ScaleControl());
        
        // 数据 
        var mountains = [
            {name: "香山", point: "116.215851,39.982685", height: "575米"},
            {name: "百望山森林公园", point: "116.234,40.008", height: "210米"},
            {name: "西山国家森林公园", point: "116.1975,39.9717", height: "300-400米"},
            {name: "北宫国家森林公园", point: "116.125,39.870", height: "约349米"},
            {name: "鹫峰国家森林公园", point: "116.083,40.067", height: "约450米"},
            {name: "凤凰岭自然风景区", point: "116.104,40.110", height: "约367米"},
            {name: "北京后花园（白虎涧）", point: "116.037372,40.121589", height: "880米"},
            {name: "白羊沟自然风景区", point: "115.950,40.200", height: "不详"},
            {name: "十三陵碓臼峪自然风景区", point: "116.233,40.317", height: "不详"},
            {name: "黄花城水长城", point: "116.333,40.400", height: "不详"},
            {name: "慕田峪长城", point: "116.567,40.433", height: "约1039米"},
            {name: "北京延庆世园公园", point: "115.970,40.447", height: "约500米"},
            {name: "昌平延寿寺", point: "116.317,40.283", height: "不详"},
            {name: "密云水库", point: "116.900,40.483", height: "约150米"}
        ];
        
        // 创建标记点数组，用于自动调整视野[3](@ref)
        var points = [];
        
        // 遍历添加标记[7](@ref)
        for (var i = 0; i < mountains.length; i++) {
            var coords = mountains[i].point.split(',');
            var point = new BMap.Point(parseFloat(coords[0]), parseFloat(coords[1]));
            points.push(point);
            
            // 创建标记[4](@ref)
            var marker = new BMap.Marker(point);
            map.addOverlay(marker);
            
            // 添加信息窗口[4](@ref)
            var infoWindow = new BMap.InfoWindow(
                "<h3>" + mountains[i].name + "</h3>" +
                "<p>海拔高度：" + mountains[i].height + "</p>" +
                "<p>状态：✅ 已征服</p>"
            );
            
            // 添加点击事件[4](@ref)
            marker.addEventListener("click", function() {
                this.openInfoWindow(infoWindow);
            });
        }
        
        // 自动调整地图视野以显示所有标记[3](@ref)
        map.setViewport(points);
    </script>
