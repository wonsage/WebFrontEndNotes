在使用Array.reduce时，要注意reduce函数每次回调都会对数组做一次遍历。
要避免在回调中直接操作第一个传参acc，如果acc是对象和数组，往往使用扩展操作符新声明一个对象或数组再返回
e.g.
```js
arr.reduce((acc, cur) => {
	let newAcc = [...acc]
	acc.push(cur+1)
}, [])
```