### 脚手架安装
vite脚手架
```
npm init @vitejs/app blog-vue3 --template vue-ts

or

yarn create @vitejs/app blog-vue3 --template vue-ts
```
vue-cli脚手架
```
npm install -g @vue/cli
vue create blog-vue3
```
> 这里我采用vite脚手架安装，毕竟vite号称更快  

```
cd blog-vue3
npm install
```
安装完成后会自动生成`shims-vue.d.ts`，这个文件是对`.vue`文件进行类型校验的声明。
```ts
declare module '*.vue' {
  import { DefineComponent } from 'vue'
  const component: DefineComponent<{}, {}, any>
  export default component
}
```
#### vue-router
```
npm i vue-router@4
```
创建`router`目录，再创建一个`index.ts`作为路由的主文件，`routes.ts`作为路由的存放路径。
```ts
// index.ts
import { createRouter, createWebHistory } from 'vue-router'
import routes from './routes'

const router = createRouter({
  history: createWebHistory(),
  routes
})

export default router
```

```ts
// routes.ts
import { RouteRecordRaw } from 'vue-router'

const routes: Array<RouteRecordRaw> = [
  {
    path: '/',
    name: 'Home',
    // .vue后缀不可省略
    component: () => import('@/view/Home.vue)
  }
]
```
#### vuex
```
npm i vuex@4
```
创建`store`目录下`index.ts`作为`vuex`主文件
```ts
import { createStore } from 'vuex'

export const store = createStore({
  state(){
    count: 1
  }
})
```
给vuex添加类型检验也需要写一个声明文件。
```ts
// shims-vuex.d.ts
import { ComponentCustomProperties } from 'vue'
import { Store } from 'vuex'

declare module '@vue/runtime-core' {
  interface State {
    count: Number
  }

  interface ComponentCustomProperties {
    $store: Store<State>
  }
}
```
#### 别名
在`import`时直接输入`../../../`是很麻烦的事情，这时候就需要使用别名。
直接配置`tsconfig.ts`中的`baseUrl`和`paths`没有生效，我也不想使用`tsconfig-path`。
所以换种思路，`vite.config.ts`中有`resolve.alias`属性用来设置别名，类似`webpack`配置。
```ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'

export default defineConfig ({
  plugin: [vue()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src')
    }
  }
})
```
#### 引入vue-router和vuex
```ts
//main.ts
import { createApp } from 'vue'
import router from './router'
import { store } from './store'
import App from 'App.vue'

createApp(App).use(router).use(store).mount('#app')
```