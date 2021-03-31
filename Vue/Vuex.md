<!--
 * @Author: your name
 * @Date: 2020-11-19 10:27:44
 * @LastEditTime: 2021-03-31 15:40:05
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \plan-A\Vue\Vuex.md
-->
### Vuex
vuex的核心就是仓库（store），包含着应用中大部分的状态(state)。  
但是vuex和全局对象不同的是：  
1、`vuex`的状态存储是响应式的。当`Vue`组件从`store`中读取状态时，如果发生变化，那么相应的组件也会得到高效的更新。  
2、不能直接修改`store`中的状态。`vuex`的状态修改只能通过显示提交(commit)`mutation`修改。  
#### State
由于`vuex`中状态是响应式存储的，所以获取状态的简单方法是在计算属性中返回状态。  
```JavaScript
computed: {
    count(){
        return store.state.count
    }
}

//为了避免取多个状态时的重复写法，可以使用mapState进行辅助
computed: {
    ...mapState({
        //箭头函数简练
        count: state => state.count,

        //传字符参数等同上箭头函数
        countAlias： "count",

        //为了能使用this获取局部状态，必须使用常规函数
        countPlusLocalState(state) {
            return state.count + this.localCount
        }
    })
}
```
#### Getters
`vuex`允许在store中定义`getters`，就像计算属性一样，`getters`的返回值会根据它的依赖被缓存起来，且只有它的依赖值发生改变才会被重新计算。  
`getter`接受`state`作为第一个参数。
```JavaScript
getters: {
    doneTodos: state => {
        return state.todos.filter(todo => todo.done)
    }
}
```
`getter`接受`getter`作为第二个参数  
`getter`可以通过属性访问，这时候getter是作为Vue响应式系统的一部分缓存其中的。  
```JavaScript
getters: {
    doneTodos: (state, getter) => {
        return getters.doneTodos.length
    }
}
store.getters.doneTodos
```
也可以通过方法访问，每次都会去调用，不会进行缓存。  
```JavaScript
getters: {
    getTodoById: (state) => (id) => {
        return state.todos.find(todo => todo.id == id)
    }
}

store.getters.getTodoById(2)
```
mapGetters辅助函数仅仅是将getters映射到部分计算属性  
```JavaScript
import {mapGetters} from 'vuex'
export default {
    computed: {
        ...mapGetters([
            'doneTodosCount',
            'anotherGetter'
        ])
    }
}
```

#### Actions
异步改变状态需要使用`action`，`action`不直接更改状态，而是发起`mutation`
#### Mutation
是改变`store`中状态的执行者，只能是同步操作。
#### Modules 
对于大型应用，可以将仓库分割成子模块。
### 通过几个问题理解vuex的原理
#### vuex的store是如何注入到组件中的？
`Vue.use(Vuex)`会调用`install`方法，装载`vuex`。  
然后看看`install`的执行逻辑。  
```JavaScript
Vue.mixin({
    beforeCreate(): {
        if(this.$options && this.$options.store){
            this.$store = this.$options.store
        }else{
            this.$store = this.$parent && this.$parent.$store
        }
    } 
})
```
综上可知，vuex的注入是通过mixin的方法，在vue构建实例时通过钩子函数`beforeCreate`注入的。
#### Getters的实现
`vuex`和`vue`一样是响应式的，`state`是通过放入`data`中实现，而`getters`是通过放入`computed`中做到响应式的。  
