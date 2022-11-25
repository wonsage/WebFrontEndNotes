Node.js可以用来构建服务器端应用和创建前端工程化工具。
JavaScript 运行在浏览器中我们就叫它客户端 JavaScript。 
JavaScript 运行在 Node.js 中我们就叫它服务器端 JavaScript。

环境变量 PATH：系统环境变量 PATH 中存储的都是应用程序路径。当要求系统运行某一个应用程序又 没有告诉它程序的完整路径时，此时操作系统会先在当前文件夹中查找应用程序，如果查找不到就会去 系统环境变量 PATH 中指定的路径中查找。

##### 全局对象`global`
模块系统
node.js的模块遵循commonJS规范。
导出：`module.exports`
导入：`require()`
使用const关键字声明导入的变量，避免导入后被修改。
#### Module Wrapper Function
- ##### `__filename` 文件名
- ##### `__dirname` 路径名
### 内置模块
node.js提供了一些有用的内置模块，如需使用其中某些方法，引入即可。
#### path
提供了一些路径操作相关的方法。
- parse()
#### fs(file system)
提供了和操作文件相关的方法。
- readdirSync()

package的安装
区分项目依赖和开发依赖

包的版本号
常见的版本号分为三部分：
如`1.2.3`分别对应了主要版本号、次要版本号、补丁版本号
`^1.2.3`要求限制版本在`1.x.x`主要版本上
`~1.2.3`要求限制版本在`1.2.x`次要版本上
`1.2.3`要求限制版本在精确的`1.2.3`版本上

更新版本号时，对应命令为`npm version major`、`npm version minor`、`npm version patch

npx命令的用途 §30
- 一次性使用的包
	如：create-react-app
- 执行本地的包
	执行当前文件夹下的node_modules文件夹中的包

#### 模块查找规则§31-33
未指定具体文件时，`.js`>`.json`>
如`require('./server')`，先将尝试查找当前目录下的、名为server的文件，`server.js`>`server.json`。如没有，再查找当前目录下的、名为server的文件夹，并查看其下的package.json中的main项的值，如没有，查找`./server/index.js'`、`./server/index.json`
未指定具体路径时
如`require('server')`，会从当前文件路径逐层向上查找node_modules文件夹

## 异步编程
#### I/O模型
- 同步I/O操作（阻塞）
- 异步I/O操作（非阻塞）
#### 进程&线程 §
计算机依靠进程为单位分配内存等资源，一个运行中的程序就对应了一个进程。而每个进程可以拥有多个线程，每个线程中是一个单一操作流。线程是进程的实际运作单位。CPU的核心越多意味着程序可同时执行的线程越多。
#### JavaScript是单线程还是多线程？§36
JS是一门同步的语言，程序按照代码顺序执行。但JS是依赖于*运行时*的，比如浏览器、node.js，而JS运行时是由底层语言编写，是支持多线程的。Node.js内部依赖了一个名为libuv的C++库，其中的线程池默认存储4个线程。
##### 回调函数
##### 使用回调函数时容易出现的问题：回调地狱§
###### 并发：`Promise.all`的使用 §42
同时调用多个Promise，各个Promise的结果按照传入顺序返回。
##### 使用异步函数`async``await`简化`Promise` §43
###### `util.promisify` §43
promisify是util下的一个方法，可以将基于回调函数的异步方法转化为返回`Promise`对象的方法。

### Event Loop 事件循环
宏任务与微任务 §
宏任务：`setInterval`、`setTimeout`、`setImmediate`、I/O。
微任务：`Promise.then`、`Promise.catch`、`Promise.finally`、`process.nextTick`。
例程 §
e.g. §49
```js
setTimeout(() => console.log("1"), 0)
setImmediate(() => console.log("2"))
// 1 2 或 2 1
```
Node.js 中，延时为0的setTimeout会被修改为1，即至少是1ms的延时执行。setTimeout的回调将在主线程的同步代码执行完毕后执行。本例中，主线程较短，执行时间有可能短于1ms，这种情况将先执行setImmediate的回调。多数情况下，`setTimeout(cb, 0)`的cb可以理解为处于宏任务列队的顶端。
e.g. §50
```js
const fs = require("fs")
fs.readFile("./index.html", () => {
  setTimeout(() => console.log("1"), 0)
  setImmediate(() => console.log("2"))
})
// 2 1
```
`fs.readFile`为异步API，