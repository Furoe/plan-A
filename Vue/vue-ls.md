### vue-ls
> Vue插件，用于从Vue上下文中使用本地storage，会话storage和内存storage。  
#### 安装
##### npm
```
npm install vue-ls --save
```
##### yarn
```
yarn add vue-ls
```
#### 使用
```JavaScript
import Storage from 'vue-ls'
options = {
    namspace: 'vuejs__', //key前缀
    name: 'ls', //命名vue变量.[ls]或者this.[$ls]
    storage: 'local', //存储名称: session, local, memory
}

Vue.use(Storage, options);
new Vue({
    el: '#app',
    mounted: function(){
        Vue.ls.set('foo', 'boo');
        Vue.ls.set('foo', 'boo', 60*60*1000); //有效时间1小时
        Vue.ls.get('foo');
        Vue.ls.get('foo', 10); //默认值10
        let callback = (val, oldVal, uri) => {
            console.log('localstorage change', val);
        }
        Vue.ls.on('foo'); //侦听
        Vue.ls.off('foo'); //不侦听
        Vue.ls.remove('foo'); //移除foo
    }
})
```