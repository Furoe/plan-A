#### ES6面试题
##### ES6新增方法面试题

###### let const var比较
var声明的变量可以提升，let、const声明的变量不能提升。
var声明同一变量可以重复声明，后声明的覆盖前面的。
let、const不能重复声明同一变量，const声明的变量值不能修改。
let、const会形成块级作用域。

###### 反引号(`)标识
可以当作正常字符使用，也可以定义多行字符串。 

###### 函数默认参数
//pass
###### [箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
箭头函数表达式比函数表达式更简洁，没有自己的this、arguments、super或new.target。
箭头函数更适用于那些本来需要匿名函数的地方，并且它不能作为构造函数。

##### 属性简写和方法简写
```JavaScript
//ES5
var student = {
	name: 'yang',
	age: '23',
	getName: function(){
		return this.name;
	}
}

//ES6
var name = 'yang';
var age = '23';
var student = {
	name,
	age,
	getName(){
		return this.name;
	}
}
```
###### Object.keys()获取对象的所有属性名或方法名
```JavaScript
Object.keys(obj);
```
###### Object.assign()源对象的属性和方法都合并到了目标对象
需要整理
###### for...of
```JavaScript
for(x of interable)
```
###### import和export
导入模块和导出模块
###### Promise对象
###### 解构赋值
###### set数据结构
###### ...(Spread Oprator)
拓展运算符
###### 字符串新增方法