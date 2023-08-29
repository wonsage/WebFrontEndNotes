#### flex布局下避免某一项超宽
```css
flex: 1;
overflow: hidden;
```
#### 限若干行数，超出省略
```scss
// 单行文本超出省略号
@mixin single-row-ellipsis {
  text-overflow: ellipsis; // 文本超出省略号
  overflow: hidden; // 超出部分隐藏
  white-space: nowrap; // 超出不换行
}

// 多行文本超出省略号 $rowCount 行数
@mixin multiple-row-ellipsis($rowCount) {
  overflow: hidden; // 超出隐藏
  text-overflow: ellipsis; // 文本超出省略号
  display: -webkit-box; // 反正你就是要加
  -webkit-line-clamp: $rowCount; // 行数
  -webkit-box-orient: vertical; // 反正你就是要加
}
```
