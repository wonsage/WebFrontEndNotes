- ### 随机排序数组
  利用sort方法
  ```
  let arr = ['a', 'b', 'c', 'd', 'e']
  arr.sort(() => { return Math.random() - 0.5 })
