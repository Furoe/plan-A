### 事件循环（Event Loop）
#### 浏览器事件循环
事件循环由执行栈、MacroTask队列、MicroTask队列组成。当执行栈执行完毕，先从MacroTask中取出一个宏任务执行，然后清空微任务队列；继续执行上序流程。
`setTimeout`、`setInterval`、`script全部`、`I/O`、`UI渲染`是MacroTask。
`Promise`、`MutationObserve`是MicroTask
#### Node事件循环
Node中的事件循环和浏览器中不同，主要体现在执行的时机。
> 外部输入数据->轮询阶段(poll)->检查阶段(check)->关闭事件回调(close callback)->定时器检测阶段(timers)->I/O事件回调阶段(I/O)->闲置阶段(Idle, prepare) 
> `setImmediate`也是宏任务，`process.nextTick`独立于这六个阶段，并优先于其它微任务
  
```js
setTimeout(() => {
  console.log('timer1')
  Promise.resolve().then(() => {
    console.log('promise1')
  })
}, 0)
setTimeout(() => {
  console.log('timer2')
  Promise.resolve().then(() => {
    console.log(promise2)
  })
})
// browser timer1->promise1-timer2->promise2
// node    timer1->timer2->promise1->promise2
```