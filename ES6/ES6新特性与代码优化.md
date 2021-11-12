### 类型转换
这个应该不算新特性，但是可以结合新特性一起优化，还是很有必要的。
因为js是动态语言，弱类型语言，所以js中的变量往往需要判断各种空值，这时使用类型转换就可以省略冗长的代码。
比如：
```js
if(x !== '' && x !== null && x !== undefined){
  // pass
}

if(!!x){
  // pass
}
```
### 可选链操作符以及空值合并操作符
ES2020新增了新的操作符`?.`和`??`，当左值为`null`或者`undefined`，返回非左值。
对于多层级的取值，如果一层一层的判断，普通的用法可能使用嵌套的判断语句，再简单点的也只是使用逻辑操作符的短路效应，但这还是不够简洁。
```js
// 一般健壮性代码
if(book){
  if(book.price){
    if(book.price.total){
      // pass
    }
  }
}

// 逻辑操作符
book && book.price && book.price.total

// 可选链调用
book?.price?.total??0
```
### 简写属性
ES6之后，对于字面量对象属性赋值，左值的变量名与非左值的变量名相等时，可以采用简化写法。
```js
let o = {
  x: x,
  y: y
}

let o = {
  x,
  y
}
```
### 简写方法
ES6之后，定义对象的属性方法时，可以省略`function`关键字以及冒号。
```js
let square = {
  area(){
    return this.side * this.side
  },
  side: 10
}
```
### 计算属性
ES6可以将表达式放在中括号中作为计算属性来使用。
```js
const PROPERTY_NAME = 'p1'
function computedPropertyName() = {
  return 'p' + 2
}

let o = {
  [PROPERTY_NAME]: 1,
  [computedPropertyName()]: 2
}
```
### 拓展操作符
ES2018及之后，使用`...`（拓展操作符）可以简化对象融合以及数组合并的操作。但是不适合在循环或者递归函数中使用，开销很大。
拓展操作符只能拓展对象的自有属性，不拓展任何继承属性。
```js
let obj = {...obj1, ...obj2}
let arr = [...arr1, ...arr2]

let o = Object.create({x: 1})
let p = {...o}
p.x // => undefined
```
### Array.of()
使用Array构造函数无法创建包含一个元素的数组，`Array.of()`可以。
```js
Array.of(10) // [10]
```
### Array.from()
将可迭代对象或类数组作为参数，生成一个新数组。
### 数组的遍历
通过使用不同的数组遍历方式，可以灵活采用不同的方法。
#### 需要可中断
在需要可中断循环时，一般使用`for`循环
```js
for(let i = 0;i < arr.length;i++){
  // pass
}

for(let x in arr){
  // pass
}

for(let x of arr){

}
```
#### 全遍历
```js
// 无返回值，且不可被break、continue中断
arr.forEach(item => item)
```
#### 返回修改后的等长数组
```js
arr1 = arr.map(item => item + 1)
```
#### 返回满足条件的子数组
```js
subArr = arr.filter(item => item > 3)
```
#### 返回满足条件的第一个元素
```js
let a = [1, 2, 3, 4, 5]
a.find(item => item === 3) // 3
```
#### 返回满足条件的第一个元素索引
```js
let a = [1, 2, 3, 4, 5]
a.findIndex(item => item === 3) // 2
```
#### 判断数组内元素是否全部满足条件
```js
let a = [1, 2, 3, 4, 5]
a.every(item => item > 3) // false
a.every(item => item < 10) // true
```
#### 判断数组内是否存在满足条件元素
```js
let a = [1, 2, 3, 4, 5]
a.some(item => item%2 === 0) // true
```
#### 归并
```js
let a = [1, 2, 3, 4, 5]
a.reduce((x, y) => x + y, 0)
a.reduce((x, y) => x * y, 1)
a.reduce((x, y) => (x > y) ? x : y)

a.reduceRight((x, y) => x + y, 0) // 从高索引开始归并 
```
### 箭头函数
```js
() => {}
x => {}
(x, y) => x + y
```