### vue-router
```JavaScript
router.push(location, onComplete?, onAbort?)
```
|声明式|编程式|
|`<router-link :to='...'>`|`router.push(...)`|
注意：如果目的路由与当前路由相同，只是参数发生变化，需要使用`beforeRouteUpdate`来响应这个变化。
```JavaScript
router.replace(location, onComplete?, onAbort?)
```
|声明式|编程式|
|`<router-link :to='...' replace>`|`router.replace()`|
`router.replace`与`router.push`很像，但是`router.replace`不会向`history`添加新纪录，而是替换掉当前`history`的记录。
```JavaScript
router.go(n)
```
类似于`window.history.go(n)`
#### 路由组件传参
```JavaScript
//pass
//后续补充，还没理解耦合问题
```
#### 导航守卫
##### 全局前置守卫
`router.beforeEach`注册全局前置守卫，当一个导航触发时，全局前置守卫是按照创建顺序调用。守卫是异步解析执行的，此时导航所在守卫的`resolve`都在等待中。
```JavaScript
const router = new VueRouter({...})
router.beforeEach((to, from, next) => {

})
```
* `to: router`：即将要进入的目标
* `from: route`：当前导航正要离开的路由
* `next: function`：resolve钩子  
* `next()`：进入管道中的下一个钩子，如果管道中钩子都执行完，导航的状态变为`confirmed`。
* `next(false)`：中断当前导航。如果浏览器URL变化了，那么URL地址会重置到`from`路由对应的地址。
* `next(error)(2.4.0+)`：导航会被终止且错误会被传递给`router.onError`的回调  

任何给定的导航守卫中，`next`函数都需要被严格调用一次。他可以出现多于一次，但是只能在所有逻辑路径都不重叠的情况下，否则钩子永远都不解析或报错。
##### 全局解析守卫
> 2.5.0+  

`router.beforeResolve`与`router.beforeEach`类似，在导航确认之前，所有组件内守卫和异步路由被解析后调用。
##### 全局后置钩子
```JavaScript
router.afterEach((to, from) => {

})
```
##### 路由独享守卫
```JavaScript
const router = new VueRouter({
  routes: [
    {
      path: 'to',
      beforeEnter: (to, from, next) => {
        //pass
      }
    }
  ]
})
```
##### 组件内的守卫
> beforRouteEnter
> beforRouteUpdate (2.2+)
> beforRouteLeave  

```JavaScript
beforeRouteEnter(to, from, next){
  // 在渲染该组件的路由没有被确认前调用
  // 不能获取组件实例this
}

beforeRouteUpdate(to, from, next){
  // 在当前路由改变，但是当前路由被复用时调用
  // 可以访问组件实例this
}

beforeRouteLeave(to, from, next){
  // 导航离开该组件的对应路由时调用
  // 可以访问组件实例this
}
```
### 完整的导航解析流程
1、触发导航
2、在失活的组件中调用`beforeRouteLeave`
3、调用全局的`beforeEach`
4、在重用的组件中调用`beforeRouteUpdate`
5、在路由配置中调用`beforeEnter`
6、解析异步路由
7、在被激活的组件中调用`beforeRouteEnter`
8、调用全局的`beforeRouteResolve`
9、导航被确认
10、调用全局`afterEach`
11、触发DOM更新
12、调用`beforeRouteEnter`中传入`next`的回调函数，创建好的组件会作为回调函数的参数传入
### 过渡动效
#### 单个路由的过渡
```JavaScript
cosnt Foo = {
  template: `
    <transition name="slide">
      <div></div>
    </transition>
  `
}

const Bar = {
  template: `
    <transition name="fade">
      <div></div>
    </transition>
  `
}
```
#### 基于路由的过渡
基于当前路由和目标路由，动态设置效果。
```JavaScript
<transition :name="transitionName">
  <router-view></router-view>
</transition>

watch: {
  '$route'(to, from){
    const toDepth = to.path.split('/').length;
    const fromDpth = from.path.split('/').length;
    this.transitionName = toDepth < fromDepth ? 'slide-right' : 'slide-left'
  }
}
```