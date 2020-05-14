#### Generator
#### yield
`yield`就是暂停标志。
`yield`后面的表达式，只有调用`next`方法，内部指针指向该语句时才执行，
等同于提供了惰性求值(lazy evaluation)。
##### next方法的参数
`yield`表达式本身是没用返回值的，或者说总是返回`undefined`。`next`方法可以带一个参数，该参数
就会被当做上一个`yield`表达式的返回值。
```JavaScript
function* foo(x){
	var y = 2 * (yield x + 1);
	var z = yield (y / 3);
	return (x + y + z);
}

var a = foo(5);
a.next()  // Object{value: 6, done: false}
a.next()  // Object{value: NaN, done: false}
a.next()  //Object{value: NaN, done: true}

var b = foo(5);
b.next()  // Object{value: 6, done: false}
b.next(12)  // Object{value: 8, done: false}
b.next(13)  // Object{value: 42, done: true}
```
##### Generator.prototype.throw()
Generator返回的遍历器对象，都有一个`throw`方法，可以在函数体外抛出错误，在函数体内捕获。
```JavaScript
var g = function* (){
	try{
		yield;
	}catch(e){
		console.log('内部捕获', e);
	}
}

var i = g();
i.next();

try{
	i.throw('a');
	i.throw('b');
}catch(e){
	console.log('外部捕获', e);
}
// 内部捕获, a
// 外部捕获, b
```
throw方法被捕获以后，会附带执行下一条`yield`表达式。相当于附带执行一次`next`。
```JavaScript
var gen = function* (){
	try{
		yield console.log('a');
	}catch(e){
		//...
	}
	yield console.log('b');
	yield console.log('c');
}
var g = gen();
g.next();  //a
g.throw();  //b
g.next();  //c
```
Generator函数体内的错误可以被函数体外的`catch`捕获。
```JavaScript
function* foo(){
	var x = yield 3;
	y = x.toUpperCase();
	yield y;
}
var it = foo();
it.next();  //{value: 3, done: false}
try{
	i.next(42);
}catch(e){
	console.log(e);
}
// uncaught type error
```
一旦Generator执行过程中抛出错误，且没有被内部捕获，就不会执行下去。
此后调用`next`，将返回`{value: undefined, done: true}`，JS引擎认为已经运行结束。
##### Generator.prototype.return()
返回给定的值，并终结遍历Generator函数。
```JavaScript
function* gen(){
	yield 1;
	yield 2;
	yield 3;
}
var g = gen();
g.next();  // {value: 1, done: false}
g.return('foo') // {value: 'foo', true}
g.next();  // {value: undefined, done: false}
```
如果Generator内部有`try...finally`代码块，并且正在执行`try`代码块，那么`return`方法会导致
立刻进入`finally`代码块，执行完以后，整个函数才会结束。
```JavaScript
function* number(){
	yield 1;
	try{
		yield 2;
		yield 3;
	}finally{
		yield 4;
		yield 5;
	}
	yield 6;
}
var g = number();
g.next();  // {value: 1, done: false}
g.next();  // {value: 2, done: false}
g.return(7);  // {value: 4, done: false}
g.next();  // {value: 5, done: false}
g.next();  // {value: 7, done: true}
```
##### yield*表达式
如果在Generator函数内部，调用另一个Generator函数。需要在前者的函数体内部，手动完成遍历。
ES6提供`yield*`表达式，用来在一个Generator函数中执行另一个Generator函数。
```JavaScript
function* foo(){
	yield 'a';
	yield 'b';
}
function* bar(){
	yield 'x';
	yield* foo();
	yield 'y';
}

//等同于
function* bar(){
	yield 'x';
	yield 'a';
	yield 'b';
	yield 'y';
}

//等同于
function* bar(){
	yield 'x';
	for(let v of foo()){
		yield v;
	}
	yield 'y';
}

```
##### yield*遍历二叉树
```JavaScript
//二叉树构造函数
//三个参数分别是左树、节点、右数
function tree(left, lable, right){
	this.left = left;
	this.lable = lable;
	this.right = right;
}

//中序遍历函数
function* inorder(t){
	if(t){
		yield* inorder(t.left);
		yield t.lable;
		yield* inorder(t.right);
	}
}

//生成二叉树
function make(array){
	if(array.length == 1){
		return new tree(null, array[0], null);
	}
	return new tree(array[0], array[1], make(array[2]));
}
let tree1 = make([[['a'], 'b', ['c']], 'd', [['e'], 'f', ['g']]]);

//遍历二叉树
var result = [];
for(let node of tree1){
	result.push();
}
```
##### 一点思考
`yield*`可以用来深度遍历，比如深拷贝，在对象上封装iterator。
##### 作为对象属性的Generator函数
```JavaScript
//简写
let obj = {
	* myGenerator(){}
}
//完整
let obj = {
	myGenerator: function* (){}
}
```
##### Generator与协程
协程(coroutime)是一种程序运行的方式，可以理解为“协作的线程”或“协作的函数”。
协程既可以用单线程实现，也可以用多线程实现。前者是一种特殊的子例程，后者是一种
特殊的线程。
###### 协程与子例程的差异
子例程采用堆栈式“后进先出”的执行方式，只有当调用的子函数完全执行完毕才会执行父函数。
而协程可以同时运行多个线程，只有一个处于运行状态，其他都处于暂停态。
###### 协程与普通线程的差异
同一时间可以有多个线程处于运行状态，但是运行的协程只能有一个，其他协程都处于
暂停状态。普通线程是抢先式的，由运行环境决定哪一个线程先得到资源。而协程是合作式的，
执行权由协程自己分配。
##### Generator与上下文
Generator函数执行产生的上下文，一旦遇到`yield`命令，就会暂时退出堆栈，但是并不消失，
里面的所有变量和对象会冻结在当前状态，等到执行`next`命令时，这个上下文环境又会加入到
调用栈，冻结的变量和对象恢复执行。
##### 异步操作的同步化表达