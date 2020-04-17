#### let
#### const
const使用的也是块级定义域，没有大括号不是块级定义域。
const实际保证的只是保存的指向地址不变，如果指向的基础类型，保存的是相应的值，但是指向的若是复杂数据类型，内容是可以修改的。
同一个变量不能多次声明，也无法在声明前取值，没有变量提升。
只要存在const关键字，就形成暂时死区。（temporal dead zoom）。
#### globalthis对象
JavaScript存在一个顶层对象，它提供全局环境（即全局作用域），所有代码都是在这个环境中运行的。但是，
顶层对象在各种实现里面是不统一的。
- 浏览器里面，顶层对象是`window`，但`Node`和`Web Worker`没有`window`
- 浏览器和Web Worker里面，`self`也指向顶层对象，但是Node没有`self`
- Node里面顶层对象是`global`，但其它环境不支持
```
(typeof window !== 'undefined'
	? window
	: (typeof process === 'object' &&
	   typeof require === 'function' &&
	   typeof global === 'object')
	? global 
	: this)
)
```