### legend
#### format
支持字符串和回调函数
e.g. `formatter: 'something{name}'` 似乎只能识别name，可以加一些其他字符
e.g. 
```js
formatter: function(name) {
      const item = data.find(i => i.name === name)
      return name + item.value
    },
```
可以访问data

### 大小位置的调整
大小和位置的配置项有width, height, left, top, right, bottom,
这些选项在grid和series下都有，grid调整的是网格，如折线图、柱状图、散点图等带有坐标轴的图表，一个echarts实例中可以包含多个grid（v2中只能有一个）。series调整的是其他类型图，如饼图、树图等，针对的是一个echarts实例包含多个图表时，控制相对位置。

### 调整坐标轴的最小刻度
`yAxis.minInterval: 1` 保证坐标轴刻度为整数