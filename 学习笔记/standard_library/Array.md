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