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