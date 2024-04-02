	BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default.
	This is no longer the case. Verify if you need this module and configure a polyfill for it.
	
	If you want to include a polyfill, you need to:

从Webpack4升级到Webpack5，出现此问题。这是因为webpack5删除了path、http等包的默认引入。
方法1：在Webpack配置中排除这几项
```json
resolve: {
	fallback: { "https": false, "zlib": false, "http": false, "url": false },
}
```
方法2：安装[node-polyfill-webpack-plugin - npm (npmjs.com)](https://www.npmjs.com/package/node-polyfill-webpack-plugin)
此包处理了path、http等node核心包的引入，适用于webpack5+.
针对某一核心包，有各自的包可以处理，如：path：path-browserify
