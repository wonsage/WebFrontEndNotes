#  JS 面试题：代码分析

##### 1. Vue/React 中为什么要在列表组件中写 key？  

   Vue 中，v-for 默认会尝试原地修改元素而非重新排序，没有 key 时，状态绑定的是位置。有 key 时，状态则根据 key 绑定到了对应的数组元素上。另外，也不能以不固定的 index 作为 key 值，key 值需要确切地指向某一唯一元素，比如 id。

##### 2.  `['1', '2', '3'].map(parseInt)` what & why ?  

   一个数组调用 map 函数，回调函数为 parseInt  
   map 函数用于使用数组生成一个新数组，每个数组元素都要经过map 的回调处理后返回。map 的回调有三个参数：currentValue、[index]、[array]。  
   parseInt 的参数则有：string、[radix]。radix 为 2~36 的进制数。以 parseInt 作为回调，则元素的 index 作为 radix 传入，因此：  
   `parseInt('1', 0) = 1` radix 为0，且字符串不以0x或0开头，则默认10进制；  
   `parseInt('2', 1) = NaN` radix 为1，不是2~36之间的数，返回 NaN；  
   `parseInt('3', 2) = NaN` radix 为2，但3不是有效的二进制数，返回NaN  

   正确做法：parseInt 作为回调时要明确其 radix，本例中即需重封装一次 parseInt。  

   ```js
   function returnInt(ele) {
       return parseInt(ele, 10)
   }
   ['1', '2', '3'].map(returnInt)
   ```

   详见：[Array.prototype.map() - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map#使用技巧案例)

3. ```JS
   let a = {n:1}
   let b = a
   a.x = a = {n:2}
   console.log(a.x)
   console.log(b.x)
   ```

   undefined  
   {n:2}

4. 找出两个数组中的重复值  

   ```js
   let arr1 = [0,1,2,3,4,5];
   let arr2 = [0,4,6,1,3,9];
   
   const commonArr = arr1.filter(item => arr2.includes(item))
   ```
   
   使用数组的过滤器判断是否属于另一数组
   
7. 
