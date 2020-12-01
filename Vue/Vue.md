### v-if 和v-show的区别
`v-if`控制节点的存在，`v-show`控制节点的`display`属性。因此`v-if`的切换成本高，`v-show`的初始渲染成本高。所以`v-if`适用于条件几乎不变的情况，而切换比较频繁的时候适合使用`v-show`。  
`v-show`不支持`<template>`元素。
### template functional
`functional`是函数式组件的一个标记，如果一个组件没有管理任何状态，也没有监听任何传给它的状态，没有声明周期方法。只是接收一些`props`的函数，在这种情况下可以将组件标记为`functional`，这表示它是无状态的(没有响应数据)，也没有实例(this上下文)。函数式组件本质上是函数，渲染开销小。
### 计算属性
计算属性是基于响应式依赖进行缓存的，只在相关依赖发生变化时进行重新计算，也就是说相关依赖没有发生变化的话会立即返回值。  
计算属性默认只有`getter`，可以在需要时添加`setter`。  
### Class绑定
```
<div class="static" :class="{active: isActive, 'text-danger': hasError}">
```
### 数组更新检测
Vue将被侦听的数组变更方法进行了包裹，这些方法会触发视图变化。
```JavaScript
push()
pop()
shift()
unshift()
splice()
sort()
reverse()
```
### 事件修饰符
```
.stop
.prevent
.capture
.self
.once
.passive

<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="submit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThis"></a>

<!-- 添加事件监听器时使用使用事件捕捉模式 -->
<!-- 即内部事件在在这处理，然后才交给内部处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只有event.target是当前元素自身时触发处理函数 -->
<a v-on:click.self="doThis"></a>
```
### 表单修饰符
#### .lazy
默认情况下，`v-model`在每次`input`事件触发后将输入框的值与数据进行同步，添加`lazy`修饰符后，只会在触发`change`事件时会同步。  
```HTML
<input v-bind.lazy="msg" />
```
#### .number
自动将输入内容转换成数值类型。
#### .trim
自动过滤首尾空白字符。
### props
#### 传入一个对象的所有`property`
如果想要将一个对象的所有`property`都作为`prop`传入，可以使用不带参数的`v-bind`。
```JavaScript
<blog-post v-bind="obj"></blog-post>
```
