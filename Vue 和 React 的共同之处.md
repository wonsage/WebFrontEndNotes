### 采用 Virtual DOM 和 diff 算法
li 元素需要指定 key 属性便于修改后的排序
### 组件的状态数据
不能直接修改，必须通过指定接口修改。
Vuex Store 通过 mutable 修改
React State 通过 setState 修改
Redux State 必须通过 Reducer 根据 Action 的描述进行修改。
这样做可以清晰地知道应用中发生了什么变化。

不同之处：
Vue组件文件扩展名是 .vue，React 组件文件扩展名依然是 .js。React 更偏向于保持原有的 js 模块形式，All in JS。
Vue 组件中结构、逻辑、样式区分更明确，对应 template、script、style。React 将HTML JS化，使其融入 JS 当中。