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