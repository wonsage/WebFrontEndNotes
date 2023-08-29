## Promise
以下是Promise的**实例方法**：
### `Promise.prototype.then()`
执行：敲定时

### `Promise.prototype.catch()`
执行：只在被拒绝（失败）时

### `Promise.prototype.finally()`

以下几个是Promise的**静态方法**：
### `Promise.all()` ★★★
参数：一个Promise对象数组
返回：一个新的Promise对象
执行：**同时开始**执行入参数组中所有的Promise。当所有promise元素 resolve后resolve，所有promise元素的返回值按原顺序组成数组返回；如有任一Promise reject，Promise.all() reject，reject reason即为该Promise的reject reason，但不影响其他Promise执行。

理解：数组中的各个Promise类似于**串联**关系（**与**关系），一个失败就失败，所有的成功才成功。

关键词：**第一个**，**失败**；**全部**，**成功**。

### `Promise.any()` ★☆☆
执行：任一promise成功后，`Promise.any()`即成功，返回结果同第一个成功的promise；如果所有promise都失败了，那么返回一个`AggregateError`类型的`Error`对象。
理解：类似于**并联**关系（**或**关系），一个成功就成功，所有的失败才失败。
关键词：**第一个**，**成功**；**全部**，**失败**。

### `Promise.race()` ★★☆
执行：任一promise被敲定后，`Promise.race()`即被敲定，返回结果同第一个被敲定的promise。
关键词：**第一个** ，**敲定**。

### `Promise.allSettled()` ☆☆☆
参数：同上
返回：同上
执行：`Promise.allSettled()`在所有promise都敲定（成功或失败）后resolve，返回一个对象数组，格式形如：`[{status: 'reject', reason: ''}. {status: 'fulfilled', value: ''}]`，表征了各个promise的结果。`Promise.allSettled()`的敲定后状态总会是resolve，不受子项promise的reject影响。
理解：适用于有多个不依赖于彼此成功完成的异步任务时，或者你总是想知道每个 promise 的结果时。
关键词：**全部**，**敲定**。

