	BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default.
	This is no longer the case. Verify if you need this module and configure a polyfill for it.
	
	If you want to include a polyfill, you need to:

从Webpack4升级到Webpack5，出现此问题：
方法1：在Webpack配置中排除这几项
```json
resolve: {
	fallback: { "https": false, "zlib": false, "http": false, "url": false },
}
```
方法2：安装[node-polyfill-webpack-plugin]([node-polyfill-webpack-plugin - npm (npmjs.com)](https://www.npmjs.com/package/node-polyfill-webpack-plugin))
