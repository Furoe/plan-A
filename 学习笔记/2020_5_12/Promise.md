#### Promise
##### Promise.prototype.then()
`then`方法返回的是一个新的`Promise`实例。
##### Promise.prototype.catch()
`Promise.prototype.catch()`是`.then(null, rejection)`或`.then(undefined, rejection)`的别称，用于指定
发生错误时的回调函数。
`then`方法指定的回调函数，如果运行中抛出错误，也会被`catch`方法捕获。
如果`Promise`状态已经变成`resolved`，再抛出错误是无效的。
##### Promise.prototype.finally()
```JavaScript
Promise.prototype.finally = function(callback){
	let P = this.constructor;
	return this.then(
		value => P.resolve(callback()).then(() => value),
		reason => P.resolve(callback()).then(() => { throw reason })
	);
}
```
