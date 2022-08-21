1. 实现一个 sleep 函数，参数为毫秒，意为等待若干毫秒，可从 Promise、Generator、Async/Await 等角度实现。  

   ```js
   function sleep(ms) {
   	return new Promise(resolve=>{
       setTimeout(resolve, ms)
     })
   }
   
   (async function () {
     console.log(a)
     await sleep(2000)
     console.log(b)
   })()
   ```

2. 手写函数实现数字数组扁平化并去重，最终得到一个升序并不重复的数组。例如：`[[1,2,3], [3,4,5,5], [6,7,8,9,[11, 12, [12,13,14]]], 10]`  

   ```js
   let arr = [ [1,2,3], [3,4,5,5], [6,7,8,9,[11,12,[12,13,14]]], 10]
   let res = []
   let obj = {}
   function unfold (arr) {
     for (let i=0; i<arr.length; i++) {
       if (arr[i] instanceof Array) unfold (arr[i])
       else {
         if (!obj[arr[i]]) {
           res.push(arr[i])
           obj[arr[i]] = true
         }
       }
     }
   }
   unfold(arr)
   for (let i=1; i<res.length; i++) {
     for (let j=i; j>0; j--) {
       if (res[j] < res[j-1]) {
         let tmp = res[j]
         res[j] = res[j-1]
         res[j-1] = tmp
       }
     }
   }
   console.log(res)
   ```

3. 手写 promise.finally

4. 手写 promise.all

5. 手写深拷贝函数

   ```js
   const isComplexDataType = obj => (typeof obj === 'object' || typeof obj === 'function') && (obj !== null) // 判断是否为对象的函数
   const deepClone = function (obj, hash = new WeakMap()) {
     if (obj.constructor === Date) return new Date(obj); // 是 Date 就新生成 Date
     if (obj.constructor === RegExp) return new RegExp(obj); // 是 RegExp 就新生成 RegExp
     if (hash.has(obj)) return hash.get(obj); // 有循环引用，就使用 WeakMap 解决
     // 以上情况均不符合，进入下面的遍历
     let cloneObj = Object.create(
     	Object.getPrototypeOf(obj),	// 原型
       Object.getOwnPropertyDescriptors(obj) // 所有自身属性的描述符
     );
     hash.set(obj, cloneObj)
     for (let key of Reflect.ownKey(obj)) {	// 遍历对象的键数组
       cloneObj[key] = (isComplexDataType(obj[key]) && typeof obj[key] !== 'function') ? deepClone(obj[key], hash) : obj[key];
     }
     return cloneObj
   }
   ```

6. ##### 什么是防抖和节流？有什么区别？如何实现？  
	
	防抖和节流都是避免短时间内大量触发的手段。

	节流(throttle)：事件触发并执行后的一段时间内的触发不会执行。节流限制了事件执行的频率上限，合并了频繁触发的事件，避免加重浏览器负担。
	- 触发后延时执行：
		```js
		function throttleDelay (func, delay) {
			let timer
			return function () {
				if (!timer) { // 如果计时器存在，不执行操作
					timer = setTimeout(() => { // 如果计时器不存在，设定计时器
						timer = null // 等待时间结束后，计时器清除
						func.apply(this, arguments) // 并执行
					}, delay) // 有效触发到执行存在等待时间
				}
			}
		}
		```
	- 触发后立即执行：
		```js
		function throttleImmediate (func, wait) {
			let timer = null
			let flag = true // 标识代表了是否能有效触发，默认为真
			return function () {
				if (flag) {
					func.apply(this, arguments)
					flag = false
					timer = setTimeout(() => {
						flag = true
					}, wait)
				}
			}
		}
		```

	   ```js
		// 利用时间戳判断
	   function throttleImmediate2 (cb, wait) {
		 let activeTime = 0
		 return () => {
		   let current = Date.now()
		   if (current - activeTime > wait) { // 第一次触发会立即执行
			 cb.apply(this, arguments)
			 activeTime = Date.now()
		   }
		 }
	   }
	   ```

	防抖(debounce)：一次有效触发后需要保持一个静默期，期间必须保持没有触发才能恢复到可执行状态。频繁触发到情况下也只是执行第一次或最后一次，相比节流而言更为精准。
	- 延时执行。一次触发后一段时间内无触发才会执行，因此只会执行连续触发中的最后一次触发。（像电梯，确保一定时间内无人进出后，电梯门关闭）
		```js
		function debounceDelay (cb, delay = 500) {
		 let timer = null
		 return () => {
		   clearTimeout(timer)
		   timer = setTimeout(() => {
			 cb.apply(this, arguments) // 确保调用参数函数 this 指向正确，而非 window
		   }, delay)
		 }
		}
		```
	- 即时执行。触发后立即执行，保持一段时间无触发，才能恢复到有效触发状态。用于点赞按钮等。
		```js
		function debounceImmediate (cb, wait = 500) {
			let timer = null
			let flag = true
			return function () {
				if (flag) {
					cb.apply(this, arguments)
					flag = false
				}
				// ⬇每次触发都会重新开始静默倒计时
				clearTimeout(timer)
				timer = setTimeout(() => {
					flag = true
				}, wait)
			}
		}
		```