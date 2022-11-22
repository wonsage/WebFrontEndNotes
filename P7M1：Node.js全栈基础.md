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
- 