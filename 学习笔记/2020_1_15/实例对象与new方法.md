#### 实例对象与new方法
JavaScript的对象体系是基于构造函数和原型链。
JavaScript使用构造方法作为对象的模板。
##### 构造函数的特点
* 函数体内部使用了`this`关键字，指向了所要生成的对象实例。
* 生成对象的时候，必须使用`new`关键字。

##### new关键字
执行构造方法，返回一个实例对象。
```
var Vehicle = function() {
	this.price = 1000;
}

var v = new Vehicle();
v.price  //1000
```
###### 限制构造函数搭配new使用
* 构造函数内部设置`use strict`，严格模式下，`this`不能指向全局对象，默认为`undefined`。
* 构造函数内部判断是否使用`new`命令，`this instanceof 构造函数`。
* 构造函数内部使用`new.target`，如果调用`new`，`new.target`指向当前函数，默认`undefined`。
##### new命令原理
1.创建一个空对象，作为将要返回的对象实例。
2.将这个空对象的原型，指向构造函数的`prototype`属性。
3.将这个空对象赋值给构造函数的`this`关键字。
4.执行构造函数内部代码。
如果构造函数内部有`return`语句，且`return`后面跟着一个对象，那么`new`返回的是`return`后面跟着的对象。否则返回`this`对象。
如果对普通函数使用`new`关键字，那么返回一个空对象。

##### Object.creat
