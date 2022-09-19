### 绑定 v-bind
### 事件 v-on
### 插槽 v-slot
初步使用：单个插槽
组件模板内某一位置添加<slot>。
使用组件时，写在组件标签的内容将插入到<slot>标签的位置。
复杂使用：多个具名插槽
简写 #
模板内多个<slot>，添加name属性区分它们，如<slot name="partA">、<slot name="partB">。
使用时，组件内容便需要多个<template>区分对应，如<template v-slot:partA>、<template v-slot:partB>。没有name的插槽，可以使用<template v-slot:default>，或直接写在组件标签内部。
v-slot只能用在<template>上。
#### 作用域插槽
插槽的作用是在父级使用子组件时按需修改组件的内容，但父级无法访问到子组件的数据。因此设置插槽时，将需要的数据绑定插槽传到父级。写法为：将数据作为v-slot的属性值。如：
**只有默认插槽时**，v-slot才可以简写到组件上。省略了<template>，还省略了参数default。
```vue
<template>
  <slot></slot>
</template>
```
```vue
<custom-comp v-slot="aDataItem">
  {{ aDataItem.name }}
</custom-comp>
```
当需要使用多个插槽时，不可以简写。
```vue
<custom-comp>
  <template v-slot:default="defaultSlot">{{ defaultSlot.someItem }}</template>
  <template v-slot:other="otherSlot">{{ otherSlot.anotherItem }}</template>
</custom-comp>
```
### v-if & v-for
v-if 和 v-for 不要用在同一个元素上
v-for 优先级比 v-if 高，因此在 for 循环的每一轮都会判断一次，重新渲染时会再次遍历整个列表。
通常两种情况

- v-if 条件用于判断是否显示整个循环
v-if 加在外层父元素上，v-for 用于子元素循环。
- v-if 条件用于筛选符合条件的项来渲染
使用 computed 来处理数据的条件筛选，而不使用 v-if。
### 子组件修改prop：`.sync`修饰符的使用
子组件需要修改父组件传来的prop是一个比较常见的场景。但是，直接在子组件修改prop是不建议的，因为
建议的方式是以事件触发的形式在父组件的事件方法中修改传入prop的源。如：

- 子组件中：`this.$emit('update:title', newTitle)`
- 父组件中：`<custom-comp :title="srcTitle" @update:title="srcTitle=$event"></custom-comp>`
Vue提供了`.sync`修饰符来简化父组件中的写法：`<custom-comp :title.sync="srcTitle"></custom-comp>`。需要注意的是，子组件中触发的事件名一定要是`update:varible`格式。

如果prop是对象，要修改的是其属性，那么有两种处理办法：

- 将对象的各个属性分别作为prop传入，并分别加上`.sync`。
- prop仍以对象传入，在子组件内生成一份其（深）拷贝，修改拷贝的属性值后，将拷贝作为参数传给事件触发函数。
```vue
<template>
<div>
	<-- 修改基本数据类型 -->
		<input "type="text" :value="title" @input="updateTitle($event)"></input>
		<input "type="text" :value="obj.name" @input="updateObj($event, 'name')" />
		<input "type="text" :value="obj.age" @input="updateObj($event, 'age')" />
</div>
</template>
<script>
import { cloneDeep } from 'lodash'
export default {
	name: '',
	props: {
		obj: Object,
		title: String,
	},
	data () {
		return {
			cloneObj: cloneDeep(this.obj)
		}
	},
	methods: {
		updateTitle (e) {
			this.$emit('update:title', e.target.value)
		},
		updateObj (e, key) {
			this.cloneObj[key] = e.target.value
			this.$emit('update:obj', this.cloneObj)
		}
	}
}
</script>
```
```vue
<template>
<div>
	<sync-child
		:title.sync="title"
		:obj.sync="obj"
	></sync-child>
</div>
</template>
<script>
import syncChild from './'
export default {
	name: '',
	components: {
		syncChild,
	},
	data () {
		return {
			title: '标题',
			obj: {
				name: 'Jhon',
				age: 18,
			}
		}
	},
</script>
```
### mixins
					   混入的顺序
					   组件内原有的>混入的，混入的按数组内先后顺序
					   data、components 会被合并，如有冲突优先组件内的
					   created等生命周期钩子会按优先级先后执行
					   methods 冲突时按优先级保留最前的