### Composition API
在Vue3.x中可以使用Composition API用法。
```ts
import { useStore } from 'vue' 

export default {
  setup(){
    const store = useStore()

    return {
      // state
      count: computed(() => store.state.count)

      // getters
      double: computed(() => store.getters.double)

      // mutations
      increment: () => store.commit('increment')

      // actions
      asyncIncrement: () => store.dispatch('asyncIncrement')
    }
  }
}
```