#### 自定义指令
部分情况，需要对普通`DOM`进行底层操作，这时候需要用到自定义指令。
```js
// 注册全局自定义指令 v-focus
Vue.directive('focus', {
  // 当被绑定的元素插入到DOM中时
  inserted: function(el){
    el.focus()
  }
})

// 注册局部自定义指令
directives: {
  focus: {
    inserted: function(el){
      el.focus()
    }
  }
}
```
##### 钩子函数
一个指令定义对象可以提供如下钩子函数：  

`bind`：只调用一次，指令第一次绑定到元素时调用，一般执行一些初始化的操作。
`inserted`：被绑定元素插入父节点时调用（仅保证父节点存在，不一定已经插入到文档）。
`update`：所在组件的VNode更新时调用，但是可能发生在其子VNode更新之前。指令的值可能发生了改变，也可能没有。但是可以通过
比较更新前后的值来忽略不必要的模板更新。
`componentUpdated`：指令所在组件的VNode和其子VNode全部更新后调用。
`unbind`：只调用一次，指令与元素解绑时调用。
##### 钩子函数参数
`el`：指令所绑定的元素，可以直接用来操作DOM
`binding`：一个对象，包含以下`property`：
* `name`：指令名，不包含`v-`前缀。
* `value`：指令的绑定值
* `oldValue`：指令绑定的前一个值，仅在`update`和`componentUpdated`钩子中可用。
* `expression`：字符串形式的指令表达式。
* `arg`：传给指令的参数，`v-my-directive:foo`中，参数为`foo`。
* `modifiers`：一个包含修饰符的对象。例如，`v-my-directive.foo.bar`中，修饰符对象为`{ foo: true, bar: true }`
`vnode`：Vue编译生成的虚拟节点
`oldVnode`：上一个虚拟节点
