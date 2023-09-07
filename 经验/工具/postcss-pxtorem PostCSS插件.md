[GitHub]([cuth/postcss-pxtorem: Convert pixel units to rem (root em) units using PostCSS (github.com)](https://github.com/cuth/postcss-pxtorem))
默认只转换字体相关样式的px

### 作为插件引入PostCSS
#### 在`vue.config.js`或`vite.config.js`中
```js
 module.exports={
    css: {
        loaderOptions: {
            postcss: {
                plugins: [
                    require('postcss-pxtorem')(option)
                ]
            }
        }
    }
}
```
写在postcss.plugins中

#### 在`postcss.config.js`中
```js
module.exports = {
	plugins: {
		'postcss-pxtorem': optionObj
	},
}
```

### 配置选项
即option对象
```json
{
    rootValue: 16, // 设计稿的字体
    unitPrecision: 5, // rem的小数位
    propList: ['font', 'font-size', 'line-height', 'letter-spacing'], // 要转换的属性
    // Array
    // 可以使用*来匹配任意字符、!反选
    selectorBlackList: [], // 要忽略的选择器，字符串数组或正则数组
    replace: true, // 直接替换，且不需要回调
    mediaQuery: false, // 转换媒体查询部分的样式
    minPixelValue: 0, // 要转化的最小px值
    exclude: /node_modules/i, // 要排除的文件
    // String
    // RegExp
    // Function
}
```