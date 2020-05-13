#### Iterator和for...of
##### Iterator遍历过程
（1）创建一个指针对象，指向当前数据结构的起始位置
（2）第一次调用指针对象的`next`方法，指向数据结构的第一个成员
（3）重复（2）直到数据结构的结束位置
##### Iterator接口和Generator函数
`Symobol.iterator`方法的最简单实现是结合`Generator`函数。
```JavaScript
let myIterator = {
	[Symobol.iterator]: function* (){
		yield 1;
		yield 2;
		yield 3;
	}
}
[...myIterator] //[1, 2, 3]

let obj = {
	*[Symbol.iterator](){
		yield 'hello';
		yield 'world';
	}
}

for(x of obj){
	console.log(x);
}
//"hello"
//"world"
```
##### 遍历器对象的return()和throw()
遍历器对象除了`next()`方法，还可以具有`return()`和`throw()`。
`return`方法的常用场合是，如果`for...of`提前结束（通常是因为出错或者有`break`），
就会调用`return`。
##### for...of
一个数据结构只要部署了`Symbol.iterator`属性，就被视作具有iterator接口，就可以用
`for...of`循环遍历它的成员。