#### Object.getPrototypeOf()
返回参数对象的原型，获取原型对象的标准方法。
``` JavaScript
var F = function(){};
var f = new F();
Object.getPrototypeOf(f) === F.prototype  //true
```
#### Object.setPrototypeOf()
接受两个参数，第一个参数是现有对象，第二个参数是原型对象。
``` JavaScript
var a = {};
var b = {x: 1};
Object.setPrototypeOf(a, b);
a.x  //1
```
#### Object.create()
以第一个参数为原型，返回一个实例对象，完全继承原型对象的属性。第二个参数是一个属性描述对象。
``` JavaScript
var obj = Object.create({}, {
	p1: {
		value: 123,
		enumerable: true,
		configurable: true,
		writable: true,
	},
	p2: {
		value: 'abc',
		enumerable: true,
		configurable: true,
		writable: true,
	}
});

//等同于
var obj = Object.create({});
obj.p1 = '123';
obj.p2 = 'abc';
```
#### Object.isPrototypeOf()
判断对象是否是参数对象的原型。
``` JavaScript
var o1 = {};
var o2 = Object.create(o1);
var o3 = Object.create(o2);

o1.isPrototypeOf(o3);  //true
o2.isPrototypeOf(o3);  //true
```
#### Object.prototype.__proto__
返回对象的原型，该属性可读写。
#### Object.getOwnPropertyNames()
返回一个数组，成员是参数对象本身的所有属性的键名，不包含继承的属性键名。
#### Object.prototype.hasOwnProperty()
用于判断某个属性定义在对象自身，还是对象的原型链。
#### in运算符
判断一个对象是否具有某个属性，不区别该属性是对象自身的，还是继承的。
#### for in
获得对象所有可遍历的属性，不管是自身的还是继承的。
#### 对象拷贝
``` JavaScript
function copyObject(orig){
	var copy = Object.create(Object.getPrototypeOf(orig));
	copyOwnProperties(copy, orig);
	return copy;
}
function copyOwnProperties(target, source){
	Object
	.getOwnPropertyNames(source)
	.forEach(function(propKey){
		var desc = Object.getOwnPrototypeDescriptor(source, propKey);
		Object.defineProperty(target, propKey, desc);
	});
	return target;
}

//ES2017
function copyObject(orig){
	return Object.create(
		Object.getPrototypeOf(orig),
		Object.getOwnPrototypeDescriptors(orig)
	);
}
```