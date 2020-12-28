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
### prop
#### 传入一个对象的所有`property`
如果想要将一个对象的所有`property`都作为`prop`传入，可以使用不带参数的`v-bind`。
```JavaScript
<blog-post v-bind="obj"></blog-post>
```
#### 禁用Attribute继承
如果你不希望组件的根组件继承`attribute`，你可以在组件的选项中设置`inheritAttrs: false`。
```JavaScript
Vue.component('my-component', {
    inheritAttrs: false
})
```
### 自定义事件
#### 将原生事件绑定到组件
#### .sync修饰符
`prop`的双向绑定，可以使用`.sync`修饰符来使双向绑定更加简洁，但是不能搭配表达式使用。
```
<text-document 
    v-bind:title="doc.title" 
    v-on:update:title="doc.title=$event">
</text-document>

<text-document v-bind:title.sync="doc.title">
</text-document>
```
### 插槽
vue 2.6 v-slot
#### 后备内容
有时为一个插槽设置默认的内容很有必要，它只会在没有提供的时候被渲染。
```JavaScript
<button>
    <slot>submit</slot>
</button>

<submit-button></submit-button> //渲染submit
<submit-button>save</submit-button>  //渲染save
```
### 动态组件
### 异步组件
#### refs
`$refs`只会在组件渲染完时生效，并且他们不是响应式的。
#### 依赖注入
`provide`选项允许执行想要提供给后代组件的数据/方法。  
负面效果就是造成了强耦合。
```JavaScript
provide: function(){
    return {
        getMap: this.getMap
    }
}
//在后代中都可以通过inject获取
inject: ['getMap']
```
### 程序化的事件侦听器
挂载第三方库的时候，需要
```JavaScript
mounted: function (){
    this.picker = new Pickaday({
        field: this.$refs.input,
        format: 'YYYY-DD-MM'
    })

    this.$once('hook:beforeDestroyed', function(){
        picker.destroy()
    })
}
```
### 循环引用
did
light
### 强制更新
`$forceUpdate`可以用来强制更新，但是`Vue`本身就是响应式，应该避免这些用法，多考虑是不是自己用错了。 
### 混入
#### 全局混入
light
light
light
light