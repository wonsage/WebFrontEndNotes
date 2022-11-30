首先说明一下几个概念：
### 进程

程序运行的一个实例，即程序运行的时候系统环境变量和用到的资源以及本身代码的集合。特点是一个CPU核心同一时间内只能运行一个进程。这对于并发来说是一个障碍，所以引入了更轻量的线程。

### 线程

线程是操作系统能够进行运算的最小单位。线程可以并发执行并共享进程中的资源。其中，并发使用了时间切片，即为每一个线程分配cpu时间，执行超过分配的时间，就强制执行下一个等待的线程。这部分是系统进行调度的，用户不需要介入。

### 并发

并发是指一段时间内（程序开始运行到结束的这段时间）执行多个程序（线程算是一个进程的子程序）。

### 协程

线程解决了进程阻塞和并发的问题，类似的，协程解决了线程阻塞和并发的问题。

不同的是，线程是为了操作系统“同时”运行更多的程序。协程是为了让一个线程内的程序并发服务更多内容。

将线程中的代码继续细分为多个任务，然后像时间片轮转一样不断去执行这些任务。不同的是，线程切换是由操作系统的时间片控制的，而协程是程序自己实现的。  
协程的切换不是按照时间来算的，而是按照代码既定分配，就是说代码运行到这一行才启动协程，协程是可以由我们程序员自己操控的。

![](//upload-images.jianshu.io/upload_images/2929041-6b0fc081dfa177a2.png?imageMogr2/auto-orient/strip|imageView2/2/w/980/format/webp)

示意图

其与线程的区别有：

-   线程可以有多个协程，但同一时间内只能运行一个协程。
-   线程是系统调度，协程是应用自己调度。
### 小结
进程>线程>协程
一个进程可包含多个线程，线程之间可以并行，线程的切换由进程调度。一个线程又可包含多个协程，协程之间互斥，一个时间只能工作一个协程，协程的切换由线程内程序自身控制。

js 主线程中运行协程的过程如下：

第一步，协程A开始执行。

第二步，协程A执行到一半，进入暂停，执行权转移到协程B。

第三步，（一段时间后）协程B交还执行权。

第四步，协程A恢复执行。

协程是一种比线程更加轻量级的存在。你可以把协程看成是跑在线程上的任务，一个线程上可以存在多个协程，但是在线程上同时只能执行一个协程。比如，当前执行的是 A 协程，要启动 B 协程，那么 A 协程就需要将主线程的控制权交给 B 协程，这就体现在 A 协程暂停执行，B 协程恢复执行；同样，也可以从 B 协程中启动 A 协程。通常，如果从 A 协程启动 B 协程，我们就把 A 协程称为 B 协程的父协程。最重要的是，协程不是被操作系统内核所管理，而完全是由程序所控制（也就是在用户态执行）。这样带来的好处就是性能得到了很大的提升，不会像线程切换那样消耗资源。

### 生成器 generator

js 中的生成器利用的就是协程，利用协程，可以实现函数暂停执行和函数恢复执行。

执行生成器的过程如下：

```jsx
function* getResult() {
    let id_res = yield fetch(id_url);
    console.log(id_res)
    let id_text = yield id_res.text();
    console.log(id_text)


    let new_name_url = name_url + "?id=" + id_text
    console.log(new_name_url)


    let name_res = yield fetch(new_name_url)
    console.log(name_res)
    let name_text = yield name_res.text()
    console.log(name_text)
}


let result = getResult()
result.next().value.then((response) => {
    return result.next(response).value
}).then((response) => {
    return result.next(response).value
}).then((response) => {
    return result.next(response).value
}).then((response) => {
    return result.next(response).value
```

可见手动执行生成器很麻烦，需要写很多重复的代码。于是有人把执行的这部分代码抽象为co.js，使用co.js只需下面这行代码：

```jsx
co(getResult()).then(res => {})
```

但是也引入了外部的代码，为了解决这个问题，ES7 引入了 async/await。

### async/await

它改进了生成器的缺点，提供了在不阻塞主线程的情况下使用同步代码实现异步访问资源的能力。其实 async/await 技术背后的秘密就是 Promise 和生成器应用，往底层说，就是微任务和协程应用。
