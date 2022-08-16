最近h5项目使用Echarts，在Android上显示正常，IOS上被图表遮挡

在 tooltip 里设置以下代码
tooltip: {
    position: function (point, params, dom, rect, size) {
        dom.style.transform = 'translateZ(0)'
    }
}
