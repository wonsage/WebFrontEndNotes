mescroll.js 是一个较为流行的、实现下拉刷新和上拉加载的JS库。

[mescroll-uni](http://www.mescroll.com/uni.html) 是它的uni-module版本，这个组件库提供了两个组件：`<mescroll-body>` & `<mescroll-uni>`，分别用于页面滚动和区域滚动。

### tip1

mescroll-uni 和竖向滚动的scroll-view一样，必须设定高度。有两种办法：

-   通过`height`属性设定高度，而非CSS。此项有值，则不使用`fixed`属性。
-   设定`:fixed="false"`。此属性默认值 true。值为false时，mescroll-uni元素高度跟随父元素，那么父元素必须有确定的高度。

### tip2

scroll-view的高度使用flex布局确定时，须设定最小高度`min-height`，比如设为0。否则竖向滚动容器的内容会溢出撑高。