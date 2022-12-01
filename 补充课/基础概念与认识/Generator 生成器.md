**生成器函数**，三种定义/声明方法：
- 使用关键字`function*`
  ```js
  function* gen() {
	  yield 10;
  }
  ```
- 使用`function*`表达式
  ```js
  const foo = function* gen() {
	  yield 10;
  }
  ```
- 使用构造函数`GeneratorFunction` 生成
  ```js
  // GeneratorFunction不是全局对象，需要从生成器函数的原型上通过constructor获取
  const GeneratorFunction = Object.getPrototypeOf(function*(){}).constructor;
  const gen = new GeneratorFunction(...args, functionBody)
  ```
  一般不使用此方法，因为此方法创建的生成器函数不会为其创建上下文创建闭包；它们始终在全局范围内创建。当运行它们时，它们只能访问自己的本地变量和全局变量，而不是从`GeneratorFunction`构造函数调用的范围的变量。
  GeneratorFunction是构造函数，生成器函数是实例。
  
**Generator对象**是生成器函数的返回值，它符合可迭代协议，是可迭代对象，可以使用for...of 遍历。
e.g.
```js
// foo: 生成器函数
const foo = function* () {
	yield 'a';
	yield 'b';
	yield 'c';
}
// gen: Generator对象
const gen = foo();
for (const val of gen) {
	console.log(val)
}
```