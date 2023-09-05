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
