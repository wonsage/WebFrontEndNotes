### 1. @表示项目根目录  
webpack打包的vue项目中，@表示src目录。
### 2. `<scroll-view>`
- 如需使用 flex 布局，必须先设`:enable-flex="true"`，否则CSS定义flex不生效。
- 使用竖向滚动时，需要给`<scroll-view>`一个固定高度，通过 css 设置 height；给子元素设置display: inline-block 或 inline-flex
- 使用使用横向滚动时，需要给`<scroll-view>`添加`white-space: nowrap;`样式。
### 3. 生命周期
有三种生命周期：
- [组件的生命周期](https://uniapp.dcloud.net.cn/tutorial/page.html#componentlifecycle)（跟Vue框架相同）
  与vue一般组件的生命周期相同，这是uni-app添加的支持，原生微信小程序不支持
- [页面的生命周期](https://uniapp.dcloud.net.cn/tutorial/page.html#lifecycle)
  
- [应用的生命周期](https://uniapp.dcloud.net.cn/collocation/App.html#applifecycle)，只针对根目录的App.vue
	- onLaunch：当`uni-app` 初始化完成时触发（全局只触发一次）
	- onShow：当 `uni-app` 启动，或从后台进入前台显示
	- onHide：当 `uni-app` 从前台进入后台
	- onError：当 `uni-app` 报错时触发
	- onUniNViewMessage：对 `nvue` 页面发送的数据进行监听
	- onUnhandledRejection：对未处理的 Promise 拒绝事件监听函数（2.8.1+）
	- onPageNotFound：页面不存在监听函数
	- onThemeChange：监听系统主题变化
### 4. `<input>`
小程序不能对DOM操作，因此无法选中原生小程序元素对象，并调用其方法。比如，无法在JS中使`<input>`聚焦。而uni-app框架的`<input>`提供了`focus`属性控制其是否聚焦。
应注意：需要聚焦时，先置虚值，在下次tick再置为真值。
```JavaScript
this.focusInput = false;
this.$nextTick(() => {
	this.focusInput = true;
});
```
### 5. `<image>`
如需获取已加载图片的宽高，使用组件原生的load方法即可。