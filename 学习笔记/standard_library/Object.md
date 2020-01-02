#### Object对象
##### 
Object对象原生的方法有两类：Object本身的方法和Object的实例方法。
###### Object本身的方法
```
Object.print = function(o){console.log(o)};
```
###### Object的实例方法
```
Object.prototype.print = function(){
	console.log(this);
};
var obj = new Object();
obj.print();  //Object
```
##### Object()
可以当作工具方法使用，将任意值转为对象。
如果参数为空，或者为`undefined`和`null`，`Object()`返回一个空对象。
如果参数是原始类型的值，`Object`方法将其转化成对应的包装对象的实例。
```
var obj = Object(1);

obj instanceof Object  //true
obj instanceof Number  //true

var obj = Object('str');

obj instanceof Object  //true
obj instanceof String  //true

var obj = Object(true);

obj instanceof Object  //true
obj instanceof Boolean  //true
```
##### Object的静态方法
`Object.keys`和`Object.getOwnPropertyNames`方法都是用来遍历对象的属性。
`Object.keys`只返回可枚举的属性，`Object.getOwnPropertyNames`可以返回不可枚举的属性。
```
var obj = ['hello', 'world'];
Object.keys(obj);  //['0', '1']
Object.getOwnPropertyNames(obj);  //['0', '1', 'length']
```
###### 对象属性模型的相关方法
* `Object.getOwnPropertyDescriptor()`：获取某个属性的描述对象
* `Object.defineProperty()`：通过描述对象，定义某个属性
* `Object.defineProperties()`：通过描述对象，定义多个属性
###### 控制对象状态的方法
* 'Object.preventExtensions()'：防止对象拓展
* 'Object.isExtensible()'：判断对象是否可拓展
* 'Object.seal()'：禁止对象配置
* 'Object.isSealed()'：判断对象是否可配置
* 'Object.freeze()'：冻结对象
* 'Object.isFrozen'：判断对象是否冻结
###### 原型链相关方法
* 'Object.create()'：指定原型对象和属性，返回一个新对象
* 'Object.getProtoTypeOf()'：获取对象的ProtoType对象
##### Object的实例方法
###### Object.prototype.valueof()
###### Object.prototype.toString()
`toString`方法作用返回一个对象的字符串形式，默认情况下返回类型字符串。
###### Object.prototype.toLocaleString()
###### Object.prototype.hasOwnProperty()
