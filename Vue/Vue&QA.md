#### 1、简述`computed`和`watch`的使用场景
当一个元素受多个元素影响，使用`computed`，例子：购物车。
当一个元素影响多个元素，使用`watch`，例子：数据搜索。
#### 2、`Vue`可以监听多个事件吗？
可以
```JavaScript
<input type="text" v-on="{input:onInput,focus:onFocus,blur:onBlur}">
```
#### 3、`$nextTick`的使用
修改了`data`里的值后马上获取这个`dom`元素的值，是取不到更新后的值的，需要使用`$nextTick`这个回调，在等待更新的值渲染成功后再获取。
#### 4、为什么`Vue`组件中`data`必须是一个函数
因为`JS`的特性，组件中的`data`写成函数相当于每个组件维护着自己的私密变量，不会互相干扰。