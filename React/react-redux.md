### react-redux
#### Provider
`react-redux`提供`Provider`使得`redux`的`store`全局可用。
```jsx
import React from 'reac'
import ReactDom from 'react-dom'

import { Provider } from 'react-redux'
import store from './store'
import App from './App'

const rootElement = document.getElementById('root')
ReactDom.render(
  <Provider store = { store }>
    <App />
  </Provider>,
  rootElement
)
```
#### connect
`connect`接收两个参数，`mapStateToProps`和`mapDispathToProps`。
```js
connect(
  mapStateToProps,
  mapDispatchToProps
)(Component)
```
如果第一个参数为空，当`store`里的`state`发生变化时，组件不会随之改变。
如果第二个参数为空，不会自动调用方法更新`store`里的`state`。