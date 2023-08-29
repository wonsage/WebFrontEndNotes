# P4M6T1：Vue 3 基础
Vue 3 的响应式性能对比 Vue 2 得到了提升。新项目开始上马 Vue 3，已有项目也考虑迁移到 Vue 3。
### 新的开发工具 §2~3
- VS Code Extension - Volar：针对 Vue 3
- Browser Extension - Vue Devtools 6.x：兼容 Vue 2/3
### 新的脚手架工具 §4
- Vue CLI (@vue/cli) 4.5.0+
- Vite 2：效率提升
	需要自行添加 eslint 支持
	1. 安装项目依赖 eslint
	2. 生成 lint 配置文件
	3. 配置 npm script 命令使用 eslint
### 组合式 API
Vue 2 中使用的是 option API，一个 Vue 组件的功能对应一个导出的选项条目，如 data、computed、methods 等。
Vue 3 带来了新的 composition API 构思，整合数据。
#### setup 选项
`setup` 的调用发生在 `data` property、`computed` property 或 `methods` 被解析之前，所以它们无法在 `setup` 中被获取。
setup 有点类似于组件的生命周期函数，它比 beforeCreate() 更早调用。
##### setup 语法糖
精简写法，省去不写 export、return 等必要操作。
多出来一个 `<script setup></script>`，内部是 setup 的逻辑代码，无需导出。
#### ref §9
需要加 `.value` 访问，这是因为使用 ref API 处理的数据会被处理为对象
##### 数组类型值
接近自然语义，没有多余的限制。
#### reactive  §10
深度响应式：对象内的所有对象都得到响应式。响应式是双向的，
无需加 `.value` 访问，这是因为框架做了自动处理，只需书写变量名，实际返回的是其 value 属性值。
##### shallowReactive §11
#### readonly §12
创建对象的深层只读代理
##### shallowReadonly §13
只对其自身属性设为只读，深层的嵌套对象不是只读的。
#### 检测方法 §13
- isProxy
- isReactive：检查对象是否是由 reactive 创建的响应式代理。包括深浅响应式。
- isReadonly：包括深浅只读。
### Refs
#### toRef
`toRef(aReactiveProxy, 'propertyName')`
#### toRefs
`toRefs(aReactiveProxy)` 将整个响应式对象转换为普通对象，并保留每个属性的响应式状态。
#### computed