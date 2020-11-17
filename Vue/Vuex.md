### Vuex
vuex的核心就是仓库（store），包含着应用中大部分的状态(state)。  
但是vuex和全局对象不同的是：  
1、vuex的状态存储是响应式的。当Vue组件从store中读取状态时，如果发生变化，那么相应的组件也会得到高效的更新。  
2、不能直接修改store中的状态。vuex的状态修改只能通过显示提交(commit)mutation修改。  
#### State
由于vuex中状态是响应式存储的，所以获取状态的简单方法是在计算属性中返回状态。  
```Vue
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
#### Actions
#### Mutations
#### Modules 