1. 错误：DELETE 请求变成了 GET 请求  
	原因：配置 axios 时，method 错写为 name
2. 错误：uncaught promise  
	原因：导入单个功能接口时，没有加 `{}`
3. 错误：请求响应异常  
	原因：必然是请求配置出错。例如，多写了某非必需项，非必需项应在需要的功能调用时写入，而不应该直接写在 data 中。
4. 错误：Uncaught (in promise) TypeError: Cannot read property 'data' of undefined  
	原因：此报错来自于请求前后的拦截器。就拉勾教育平台项目来说，请求或其上层封装某函数没 return。详见：[Uncaught (in promise) TypeError: Cannot read property 'data' of undefined_十眠的博客-CSDN博客](https://blog.csdn.net/qq_38983511/article/details/103674826)
5. 错误：[Vue warn]: Error in nextTick: “RangeError: Maximum call stack size exceeded 
	原因：出现死循环。常见于在Vue模块的模板内书写了模块HTML标签。
6. 错误：'props' is not defined  no-undef
	原因：函数组件没有入参 props；类组件调用参数时没有写 this。
7. 错误：## Uncaught TypeError: Cannot read  properties of undefined (reading ‘setState’)
	原因：this 指向不明，默认为 undefined，因此无法调用到 setState。使用箭头函数即可。