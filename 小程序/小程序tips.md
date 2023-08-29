### 1、swiper 组件
current属性指示了当前展示的图片序号。如果出现swiper数据源替换的操作，比如刷新，而恰好current大于新数组的长度，就会产生报错：`[swiper] current无效,请修改current值。`
因此需要注意再替换数据源前将current值修改为0.