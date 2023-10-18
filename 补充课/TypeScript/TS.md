语言的类型
根据类型安全的不同可分为：
强类型：不允许任意的数据隐式类型转换
弱类型：几乎
根据类型检查的差异可以分为：
静态类型：声明时即确定变量的类型，且后续无法再改变。
动态类型：只有在运行阶段才能确定变量的类型，且变量的类型也可以随时改变。

JS是解释型语言（脚本语言），不存在单独的编译阶段，报错信息只会在运行时出现。它是一种动态类型语言。
TS提供了类型的校验，它需要先编译为JS，编译过程中会提示错误信息，避免线上发生错误。它是一种静态类型语言。

### 类型声明
```ts
let num: number = 1

let str: string = 'abc'

let bl: boolean: false

let var1: number | string = '123'

let var2: any = true

function fn(text: string): void { // void 指明函数的返回值为空
	console.log(text)
}
```
类型有：number、string、boolean、
#### void
表示没有任何类型，通常用于指明函数返回值。声明一个void类型的变量，则只能赋予`undefined`和`null`。
#### null、undefined
这两个的特殊性在于，它们既是类型，也是值。
同`void`类型一样，这两个类型用处不是很大，一般不用来声明。
默认情况下`null`和`undefined`是所有类型的子类型，比如可以把 `null`和`undefined`赋值给`number`类型的变量。
指定了`--strictNullChecks`标识时，null和undefined则只是void的子集，即只能将`null`和`undefined`只能赋值给`void`和它们各自类型。
#### never
永不存在的值。
常见于指明函数的返回值，如：
```ts
function error(message: string): never {
	throw new Error(message);
}
function infiniteLoop(): never {
	while (true) {
	}
}
```
以上两个函数的返回值为never，那么该函数必须存在无法到达的终点，比如死循环或者抛出错误。
#### 值类型
单个值也是一种类型，是对应数据类型的子类型
如`const a = 5`，常量a会被推断为值类型5，值类型5是number类型的子类型。
`let b: number;` `b = a;`正确
被声明为值类型的变量只能赋该值。
通常用在联合类型中，用来确定具体的值。
#### 联合类型 union types
支持联合类型：使用`|`连接多个类型
联合类型相当于类型的自由组合，提高了自由度。
##### 使用
- 既可以是数字也可是字符串`let setting:number|string`
- `let gender:'male'|'female'`
- 固定可数情形的值`let choice:true|flase`
- 结合字面量类型和值类型：`let v:string|5`
- 在打开了strictNullChecks时，常用`let name:string|null`

除any和联合类型外，变量声明为某一类型后，会对其进行类型校验，如果赋值的类型错误会报错。
### 字面量类型与包装对象类型
原始类型包括了 string、number、boolean、bigint、symbol这五种，它们都有字面量和包装对象两种情况。
其中，string、number、boolean都可以使用构造函数生成一个包装对象类型，如`let n = new Number()`。
在TypeScript中，为了区分这两种情况，区分了大小写的`string`和`String`。
小写的只包含字面量，大写的包含字面量和包装对象。
在很多内置方法的参数，ts已经定义为小写类型，如果传入大写类型会报错，所以一般情况都建议使用小写类型。
### Object 与 object
`Object` 广义对象，包括数组、函数，还包括原始类型的包装对象，不包括null和undefined。可以简写为`{}`。
`object` 狭义对象，只包含数组、函数、对象。
二者都只包含原生Object对象，自定义的类型不在其中，因此不能使用
### 接口 interface
接口，顾名思义，用以定义一种使用规范。以此接口作为类型声明的变量就需要满足接口的定义。（类似于class的概念)
```ts
interface Person {
	name: string,
	age: number,
	address?: string, // 可选属性
	readonly warzdrun: number, // 只读属性
	[propName: string]: boolean, // 任意属性（这里键名必须为字符串，键值必须为布尔
}
let p1: Person {
	name: 'Tom',
	age: 12,
}
```
### 数组
```ts
let numArr: number[] = [1,2,3,4] // 成员必须为数值

let strArr: string[] = ['a', 'b', 'c'] // 成员必须为字符串
let anyArr: any[] = [1, 'a', true]

```