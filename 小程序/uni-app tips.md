### -   @表示项目根目录  
webpack打包的vue项目中，@表示src目录。
### -`<scroll-view>`
	-   如需使用 flex 布局，必须先设`:enable-flex="true"`，否则CSS定义flex不生效。
	-   使用竖向滚动时，需要给 <scroll-view> 一个固定高度，通过 css 设置 height；  
	    给子元素设置display: inline-block 或 inline-flex
	-   使用使用横向滚动时，需要给`<scroll-view>`添加`white-space: nowrap;`样式。

-   生命周期

有三种生命周期

-   组件的生命周期（跟Vue框架相同）
-   页面的生命周期
-   应用的生命周期，只针对根目录的App.vue