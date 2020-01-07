##### Array对象
###### 静态方法
Array.isArray()
```
var arr = [1, 2, 3];
Array.isArray(arr)  //true
```
###### 实例方法
valueOf()
```
var arr = [1, 2, 3];
arr.valueOf()  //[1, 2, 3]
```
toString()
```
var arr = [1, 2, 3];
arr.toString()  //1, 2, 3

var arr = [1, 2, 3, [4, 5], 6];
arr.toString()  //1, 2, 3, 4, 5, 6
```
push()
在数组末端添加一个或多个元素，返回添加新元素之后的数组长度。
```
var arr = [];
arr.push(1)  //1
arr.push('a')  //2
arr.push(true, {})  //4
arr  //[1, 'a', true, {}]
```
pop()
删除数组最后一个元素，并返回该元素。
```
var arr = ['a', 'b', 'c'];
arr.pop()  //'c'
arr  //['a', 'b']

[].pop()  //undefined
```
shift()
删除数组第一个元素，并返回该元素
```
var arr = ['a', 'b', 'c'];
arr.shift()  //'a'
arr  //['b', 'c']
```
unshift()
在数组头部添加一个或多个元素
join()
以指定参数作为分隔符，将所有数组成员连接成一个字符串返回，默认用逗号分隔。
```
var arr = [1, 2, 3];
arr.join()  //'1, 2, 3'
arr.join('|')  //'1 | 2 | 3'
```
如果数组成员是`undefined`或`null`或空位时，会转换成空字符串。
concat()
用于多个数组合并，将新数组成员添加到原数组成员的后部，然后返回一个新数组，原数组不变。
如果数组成员包含对象，那么concat方法返回的是数组的浅拷贝。
```
var obj = {a: 1};
var oldArray = [obj];
var newArray = oldArray.concat();

obj.a = 2;
newArray[0].a  //2
```
reverse()
slice()
```
arr.slice(start, end)
Array.prototype.slice().call({0: 1, 1: 2, length: 2}); //[1, 2]
```
splice()
删除数组部分元素
```
arr.splice(start, count, addElement1, addElement2, ...);
var a = [1, 2];
a.splice(1, 0, 3);
a  //[1, 3, 2]
```
sort()
默认按照字典顺序进行排序
```
[11, 101].sort()  //[101, 11]
[10111, 1101, 111].sort()  //[10111, 1101, 111]

[10111, 1101, 111].sort(function(a, b){
	return a - b;
});
//[111, 1101, 10111]
```
map()
将数组所有成员依次传给参数函数，然后把每次执行结果拼成新数组返回。
```
var numbers = [1, 2, 3];
numbers.map(function(n){
	return n + 1;
});
//[2, 3, 4]
numbers  //[1, 2, 3]
```

```
var arr = ['a', 'b', 'c'];
[1, 2].map(function(e){
	return this[e];
}, arr);

//this绑定map的第二个参数
//['b', 'c']
```
forEach()
类似于map()
filter()
filter用于过滤数组成员，满足条件的成员组成一个新数组返回。
```
[1, 2, 3, 4, 5].filter(function(elem){
	return (elem > 3)
});

var obj = {MAX: 3};
var myFilter = function(item){
	if(item > this.MAx) return true;
};
[1, 2, 3, 4, 5].filter(myFilter, obj);
```
some()和every()
返回一个布尔值，判断数组成员是否满足某个条件
some：只要一个成员的返回值是true，则整个some返回的是true。
every：只有每个成员的返回值是true，才返回true。
reduce()和reduceRight()
依次处理数组成员，累计成一个值。
如果要对累计变量指定初值，可以把它放在reduce和reduceRight的第二个参数处。
indexOf()和lastIndexOf()
返回给定元素在数组中第一次出现的位置，如果没有返回-1。