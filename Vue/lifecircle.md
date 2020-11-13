#### Vue的生命周期
Vue的生命周期分为beforeCreate、created、beforeMount、mounted、beforeDestroy、destroyed。
##### vue的源码
分析生命周期，我们首先得从创建vue实例开始。  
在`new Vue()`的时候，`vue/src/core/instance/index.js`中的`_init()`负责初始化各个功能。
```Javascript
function Vue(options){
    if(process.env.NODE_ENV !== 'production' && !(this instance Vue)){
        warn('Vue is a constructor and should be called with the `new` keyword');
    }
    this._init(options);
}
```
`_init`中的执行顺序为下
```JavaScript
initLifeClircle(vm)
initEvents(vm)
initRender(vm)
callHook(vm, 'beforeCreate')
initInjections(vm)  //resolve injections before data/props
initState(vm)
initProvide(vm)  //resolve provide after data/props
callHook(vm, 'created')
```
而在`initState()`中
```JavaScript
if(opts.props) initProps(vm, opts.props)  //初始化props
if(opts.methods) initMethods(vm, opts.methods)  //初始化methods
if(opts.data) {
    initData(vm.data);
}else{
    observe(vm.data = {}, true, /* as root data*/);  //初始化data
}
if(opts.computed) initComputed(vm, opts.computed);  //初始化computed
```