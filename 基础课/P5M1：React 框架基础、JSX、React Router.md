# P5M1：React 框架基础、JSX、React Router
## 创建 React 项目
### 方法一：自定义 Webpack 搭建 #2
重点在于 webpack.config.js 的配置：
```js

```

### 方法二：使用脚手架快速创建 #3
全局安装 create-react-app
命令行创建项目
## JSX
JSX（JavaScript XML）可以看作是 JS 的语法扩展。它实现了在 JS 中写 HTML 标记语言，并可以被转为 HTML 在界面展示。它需要在 React 框架支持下使用。

- 动态显示变量
	```JSX
	function () {
		let name = 'JSX'
		return (
			<div>
				<p>{name}</p>
			</div>
		)
	}
	```
- 调用方法，内置方法和自定义方法均可。
- 支持表达式，如三元表达式
	```jsx
	let boolean = true
	<p>{boolean ？ '是' : '否'}</p>
	```
- 模板字符串

#### 注意要点 #5
- 对象不能直接显示，需要先 .stringfy
- 元素的属性
	- 字符串属性值以 `""` 包裹。
	- 表达式动态值用 `{}` 包裹，不再带 `""`，如 `<p titil={p.name}></p>`。
		这点与 Vue 不同，Vue 的页面结构是传统的HTML存在，而非 JSX 对象。
- 只能有一个根元素
- 单标签必须正确关闭
	e.g. `<img />`
#### 其他特性
- React DOM在渲染JSX时默认会转义，可以有效防止XSS 攻击
- JSX 对象会被转译为 `React.createElement()` 的函数调用，它会创建出 **React 元素**对象。
	
#### 事件操作 #6
##### 事件绑定
`<button onClick={handler()}></button>`
第一个参数默认就是事件对象 ev，函数内可以直接调用。
##### 事件监听传参
- 使用箭头函数返回：`<button onClick={() => {handler(1, 2)}>点击事件</button>`
	若需要获取事件对象：`<button onClick={(ev) => {handler(ev)}}>点击事件</button>`
- 使用 bind 返回一个新函数：`<button onClick={handler.bind(null, 1, 2)}>点击事件</button>`
	有传参时，默认最后一个参数是 ev，函数内可以直接调用。
#### 数据的遍历 #7
一个数组能够被解构为单个成员组成的字符串，不能直接被解析分离为单个元素。
需要调用 map 方法，每个成员都做一次返回。
### 样式
#### 内联式 #8
- JSX 中的 CSS 其实是作为对象存在，因此它需要按照JS的语法来写，而非CSS语法。
	```JSX
	const styleObj = {
		width: 100,
		height: 200,
		backgroundColor: 'green'
	}
	function App() {
		return(
			<div style={styleObj}>Style</div>
		)
	}
	```
	每组逗号结尾而非分号；改为驼峰命名法；字符串类型的属性值引号包括。
	多个样式对象时，使用样式对象数组。
不支持伪类和媒体查询设置，需引入第三方包，如radium。
#### 外联式 #9
全局外联样式
创建一个模块和.css文件，css引入模块，模块引入index.js
模块样式
导入css文件时使用一个变量接收

自定义元素
```js
const SectionDiv = 
	  
```
### 组件
React 的组件其实就是单个的函数，返回了一个 JSX 对象或者说 React DOM 对象。
这样的一个组件在被定义后，便可作为自定义组件用在其他 JSX 中。
##### 定义组件
React 组件有两种形式的定义方法：
- 函数组件
	```JSX
	function CustomizeComp(props) {
		return <h1>Hello, {props.name}</h1>
	}
	```
- class 组件
	```JSX
	class CustomizeComp extends React.Component {
		render() {
			return <h1>Hello, {props.name}</h1>
		}
	}
	```
	一个继承自 React.Component 的类，拥有 render 方法。

上面两种定义都是可以的，也是等效的。
自定义组件名必须以**大写字母**开头，通常采用大驼峰命名法（这点也与JS 中的类名规范相同）。小写字母开头的元素代表着HTML 内置元素。自定义组件和原生元素在 React 中的处理是不同的。
### 组件的 props
组件的 props 包含了JSX所接收到的所有属性和子组件对象。
#### 从 props 中取属性值 #11
自定义组件往往有着自定义的属性和子组件。它们以 props 对象的形式传入，取值时使用 props 调用即可。
```JSX
// 子组件A
function ChildA(props) {
	return (
		<div>
			<p>{props.person.name}</p>
			<p>{props.person.age}</p>
		</div>
	)
}
// 子组件B
function ChildB(props) {
	return (
		<div>
			<p>{props.words}</p>
		</div>
	)
}
// 父组件
function Father(props) {
	return (
		<div>
			<ChildA person={props.author} />
			<ChildB words={props.quote} />
		</div>
	)
}
// 数据
const obj = {
	objP: {
		name: 'Jack',
		age: '12'
	},
	text: 'Life is good and bad.'
}
// 渲染
ReactDOM.render(
	<Father
		author={obj.objP}
		quote={obj.text} />,
	document.getElementById('root')
)
```
这段示例代码中，可以看到，子组件从父组件取值时，对应的是它在父组件下使用的属性名。
上面这一写法是通过属性单独传递，还可以通过整个对象解构后传递：
```JSX
function ChildApp() {
	return (
		<div>
			<p>{name}</p>
			<p>{age}</p>
		</div>
	)
}
function App() {
	return ({
		<div>
			<ChildAPP {...obj} />		
		</div>
	})
}
const obj = {
	name: 'Jack',
	age: 15
}
```
其实就是把一个对象整个传递给子组件，子组件直接取用对象下的键值，无需再通过属性名确定对应关系。

#### 组件 props 的默认值和类型校验 #12
默认值设置两种组件有些许不同：
- 函数组件
	`ComponentName.default`
- 类组件
	类中设置 `static defaultProps`

类型校验需要第三方包 prop-types 支持：
```JS
ComponentName.propTypes = {
	name: PropTypes.string.isRequired, // 强制要求，error
	age: PropTypes.number // 校验，warning
}
```
#### 从 props 取子组件（JSX） #13
一个自定义组件在其内容中直接添加子组件是无法得到支持的，如：
```JSX
<div>
	<CustomizeComp name='father'>
		<p>ChildComp</p>
	</CustomizeComp>
</div>
```
此时，写在内容中、而非写在定义中的子组件不会显示。
这一子组件也可以被视为当前组件父组件的传入对象，在 props.children 访问，需要在定义中添加。
### 【实例】组件布局 #14
### 组件的 state
状态 state 是组件的私有数据。状态数据必须通过 setState() 修改，能引起 React 对视图的重新渲染，也即数据驱动视图。
setState 的注意事项
setState 可以传入对象，对state 对象浅覆盖，这种更新可能会被合并，不能第一时间反映。
也可以传入回调函数。
- 是异步的
	解决办法有两种：
	- async await
	- 添加回调函数作为 setState 的第二个入参
- 注意 this 的指向
	调用了 setState() 的方法，this 需要绑定，否则是 undefined。
	- 传统函数写法，但在事件回调中使用箭头函数
		e.g. `<button onClick={() => this.handleClick()}></button>`。
		此语法问题在于每次渲染组件时都会创建不同的回调函数。如果该回调函数作为 prop 传入子组件时，这些组件可能会进行额外的重新渲染，带来性能问题，因此不推荐。
		也可以：`<button onClick={this.handleClick.bind(this)}></button>`
	- 传统函数写法，但记得在 constructor 中做绑定。
		e.g. `this.handleClick = this.handleClick.bind(this)`
	- 写成箭头函数【推荐】
#### 单向数据流 #18
数据都是向下流动的，即从父组件向子组件传递，子组件无法向父组件传值。
基于单向数据流，我们需要共享的数据需要放在上层组件（上游）。
子组件如要修改共享过来的数据，必须调用与数据同样共享过来的方法（当然这一方法中也是调用 setState() 修改的）。
#### 表单
经典HTML 表单元素通常自己维护 state，因为它们需要根据用户输入来进行更新。React 同样支持经典表单元素，但是 React 更标准的写法是受控组件，即以 React state 为唯一数据源的表单元素。
##### 受控组件
###### text 类型的 input & textarea
只使用 state 的值，但不希望使用 state 来管理表单数据的情形：
- readOnly：设置只读，无法修改。
- defualtValue：设置为默认值，只是用于展示。
###### select 下拉菜单
###### 单选框、复选框
##### 非受控组件
非受控表单也可以在 React 中使用。它们的值是存放在 DOM 元素中的，不受 React 管理，取值时需要操作 DOM 元素。
### 生命周期
##### 挂载 #32
1. **`constructor()`**
2. `static getDerivedStateFromProps()`
3. **`render()`**
4. **`componentDidMount()`**：在组件已经被渲染到 DOM 中后运行。
##### 更新 #33
1. `static getDerivedStateFromProps()`
2. `shouldComponentUpdate(nextProps, nextState)`：控制组件是否更新
	- 参数：
		- nextProps：
		- nextState：
	- 返回值：默认 true。若返回 false，则后续方法不再执行。
1. **`render()`**
2. `getSnapshotBeforeUpdate()`
3. **`componentDidUpdate()`**：组件渲染后执行。
	
##### 卸载 #34
- **`componentWillUnmount()`**
	- 应用：在组件被卸载及销毁**前**执行。常用于清理操作，如：清除 timer，取消网络请求或清除在 `componentDidMount()` 中创建的订阅等
	- 注意：当中不应含有 setState()，因为组件实例卸载后不会再次挂载，修改状态不会得到重新渲染。

### mock
#### GET 请求的简单处理 #37
### Redux
Redux 是一个状态管理模块，可以搭配 react 使用，针对更为复杂的组件数据处理和通信。
它能带来的便利在于：
- 某个组件的状态，需要共享
- 某个状态需要在任何地方都可以拿到
-  一个组件需要改变全局状态
-  一个组件需要改变另一个组件的状态
Redux 是一个独立的包，不过专门为 React 写了 react-redux，某些 API 与原生 Redux 略有不同。

Store 是整个应用的状态容器，State 是某一时刻容器中的状态，State 对应了 View。
Reducer 是产生新状态的方法，也可以产生状态容器。Reducer 中包含了数据和条件判断逻辑。
Store 调用 Action 来修改 State。

将 createStore 方法 引入