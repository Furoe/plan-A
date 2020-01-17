#### 对象的继承
JavaScript的继承，通过“原型对象”(prototype)实现。
##### 构造函数的缺点
同一个构造函数的多个实例之间，无法共享属性，从而造成资源浪费。
##### prototype属性的作用
原型对象的所有属性和方法，都能被实例对象共享。
JS规定每个函数都有一个prototype属性，指向一个对象。
```
function f(){}
typeof f.prototype  //"Object"
```
普通函数不会用到这个属性，但是构造函数在生成实例时，该属性会自动成为实例对象的原型。
##### 原型链
JS规定，所有对象都有自己的原型对象。任何一个对象都可以成为另一个对象的原型，因此构成一个原型链。
原型链的尽头是null。
##### constructor属性
`prototype`对象有一个`constructor`属性，默认指向`prototype`所在的构造函数。
修改原型对象的同时，一般需要修改`constructor`属性，防止引用错误。
```
function Person(name){
	this.name = name;
}

Person.prototype.constructor === Person  //true
Person.prototype = {
	method: function(){}
};

Person.prototype.constructor === Person  //false
Person.prototype.constructor === Object  //true
```
##### 多重继承
JS不提供多重继承功能，不允许一个对象同时继承多个对象。
可以通过Mixin(混入)解决。
```
function M1(){
	this.hello = 'hello';
}

function M2(){
	this.world = 'world';
}

//继承M1
S.prototype = Object.create(M1.prototype);
//在S继承链上加上M2
Object.assign(S.prototype, M2.prototype);
S.prototype.constructor = S;

var s = new S();
s.hello  //'hello'
s.world  //'world'
```
##### 封装私有变量：立即执行函数写法
将相关的属性和方法封装在一个函数作用域里。
```
var module1 = (function (){
	var _count = 0;
	var m1 = function(){
		//...
	};
	var m2 = function(){]
		//...
	};
	return {
		m1: m1,
		m2: m2
	};
})();
```
##### 模块的放大模式
如果一个模块很大，要分成几个部分，或者一个模块要继承另一个模块，这时就有必要采用放大模式(augmentation)。
```
var module1 = (function(mod){
	mod.m3 = function(){
		//...
	};
	return mod;
})(module1);
```
##### 宽放大模式(Loose Augmentation)
```
var module1 = (function(mod){
	return mod;
})(window.module1 || {});
```