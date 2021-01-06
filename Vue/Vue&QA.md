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
#### 5、`delete`和`Vue.delete`的区别
`delete`只是将数组被删除的元素置为`empty`或`undefined`，不改变键值，而`Vue.delete`是直接删除了数组，改变了数组的键值。
#### 6、`Vue`里面的`router-link`在电脑上有用，在安卓上没反应怎么解决
`Vue`路由在安卓上有问题，`babel`问题，安装`babel-polyfill`插件解决。
#### 7、`Vue2`中注册在`router-link`上的事件无效
使用`@click.native`，因为`router-link`会阻止`click`事件，`.native`直接监听原生事件。
#### 8、`RouterLink`在IE和Firefox中不起作用
方法一：只使用`a`标签，不使用`button`。
方法二：使用`button`标签，用`Router.navigate`跳转。
#### 9、`active-class`是哪个组件的属性
`vue-router`模块的`router-link`组件，`children`数组定义子路由。
#### 10、`vue-router`有哪几种导航钩子
1、全局导航守卫`router.beforeEach(to, from , next)`，跳转前进行判断拦截。
2、组件内的守卫
3、单独路由独享守卫