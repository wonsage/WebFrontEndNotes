1. 安装postcss和postcss-pxtorem
   `npm i postcss`
   官网地址：[postcss.org/](https://link.juejin.cn/?target=https%3A%2F%2Fgitee.com%2Flink%3Ftarget%3Dhttps%253A%252F%252Fpostcss.org%252F "https://gitee.com/link?target=https%3A%2F%2Fpostcss.org%2F") 
   github地址：[github.com/postcss/pos…](https://link.juejin.cn/?target=https%3A%2F%2Fgitee.com%2Flink%3Ftarget%3Dhttps%253A%252F%252Fgithub.com%252Fpostcss%252Fpostcss "https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Fpostcss%2Fpostcss")
   `npm i postcss-pxtorem -D`
   [cuth/postcss-pxtorem: Convert pixel units to rem (root em) units using PostCSS (github.com)](https://github.com/cuth/postcss-pxtorem)
   
   注意包的版本，postcss-pxtorem@6依赖postcss@8依赖webpack@5，postcss-pxtorem@5依赖postcss@7依赖webpack@4。
2. 配置postcss.config.js文件
   
3. 定义HTML根元素的font-size
   使用设计稿宽度下以vw为单位的rootValue尺寸
   过去，动态的html font size有两种做法：
   1. 使用媒体查询。缺点是不能随着窗口宽度连续变化。
   2. 使用mefe-flexible或自己写一段函数通过监听窗口变化来修改root font size。
   3. 目前vw单位已经在主流浏览器普遍支持，使用vw即可实现连续变化。

与其他实现方案的区别
- scale通过缩放
  优点：快速简单
  缺点：纵横比锁定，其他比例的屏幕上会留空；模糊；点击错位。
