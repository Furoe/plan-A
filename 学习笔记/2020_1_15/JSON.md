#### JSON
##### JSON规定
> * 复合类型的值只能是数组和对象，不能是函数、正则表达式对象、日期对象。
> * 原始类型的值只有四种：字符串、数值（必须以十进制表示）、布尔值和null。（不能使用NaN、+Infinity、-Infinity和undefined）
> * 字符串必须用双引号表示，不能用单引号。
> * 对象的键名只能放在双引号里。
> * 数组或对象最后一个成员的后面不能加逗号。
##### JSON对象
`JSON`对象是JavaScript的原生对象，有两个静态方法`JSON.stringify`和`JSON.parse`.
###### JSON.stringify
会忽略对象不可遍历的属性
###### 参数对象的toJSON方法
如果参数对象有自定义的toJSON方法，那么`JSON.stringify`会使用这个方法返回值。
```
var user = {
	firstName: '三',
	lastName: '张',
	get fullName(){
		return this.lastName + this.firstName;
	},
	toJSON: function(){
		return {
			name: this.lastName + this.firstName;
		}
	}
}
JSON.stringify(user)  //"{"name": "张三"}"
```