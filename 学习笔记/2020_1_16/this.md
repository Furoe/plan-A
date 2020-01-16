#### this关键字
`this`总是返回一个对象
设计目的：在函数内部，指代函数当前运行环境
```
(obj.foo = obj.foo)()  //window
(false || obj.foo)()  //window
(1, obj.foo)()  //window
```
##### 避免多层this
```
var o = {
	f1: function(){
		console.log(this);
		var f2 = function(){
				console.log(this);
			}();
	}
}
o.f1
//Object
//window
```
##### 避免回调函数中的this
##### 绑定this的方法
###### Function.prototype.call()
```
var obj = {};
var f = function(){
	return this;
}
f() === window  //true
f.call(obj) === obj  //true
```
###### Function.prototype.apply()
###### Function.prototype.bind()