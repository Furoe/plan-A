#### Vue的生命周期
Vue的生命周期分为beforeCreate、created、beforeMount、mounted、beforeDestroy、destroyed。
##### vue的源码
分析生命周期，我们首先得从创建vue实例开始。  
在`new Vue()`的时候，`vue/src/core/instance/index.js`中的`_init()`负责初始化各个功能。
```Javascript
function Vue(){
    if(process.env.NODE_ENV !== )
}
```