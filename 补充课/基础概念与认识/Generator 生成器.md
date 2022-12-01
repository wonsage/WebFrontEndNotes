生成器函数，三种定义/声明方法：
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



