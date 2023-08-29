## JS 概念考察
##### var、let、const的区别  
   let和const是ES6新加入的关键字，用来声明变量和常量。由于ES6规定的块级作用域的关系，let定义的变量只能在块级作用域内访问，不能跨块或跨函数，而var定义的可以。同一个块内，let声明的变量不能再次被声明，而var的可以。另外，let没有变量提升，变量必须在定义后使用。  
   关于const，const声明时必须要赋初值，且不能再被修改。const是一个对象的话，对象的值是可以修改的。
##### ES6新增  
- let、const
- 数组和对象的解构
- 箭头函数
- 模板字符串
- 计算属性名  
	`{[variable]: value}`
- 新对象和构造函数：Proxy、Reflect
- Set & WeakSet、Map & WeakMap
##### 说说 Set、WeakSet、Map、WeakMap 的区别：  

   ES6 提供的 Set 类似于**数组**，有键值无键名，但其成员的值都是唯一的，没有重复值。  
   WeakSet 与 Set 的区别在于，WeakSet 的成员只能是对象。另外，WeakSet 中的对象都是弱引用，即如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。正因为其弱引用特性，WeakSet 不存在未取消引用导致内存无法释放的问题，也无法确定WeakSet 内部的成员数量，因此无法遍历。  
   Map 类似于**对象**，也是键值对的集合，但Map 可以以任意数据类型作键，而对象只能以字符串作键。  
   WeakMap 与 Map 的区别有两点：WeakMap 只接受对象作为键名（null 除外）；WeakMap 的键名对象不计入垃圾回收机制。

