#### 任务队列
任务队列存在多个，同一任务队列内，按队列顺序被主线程取走；不同任务队列间，存在优先级，优先级高的优先执行。
##### 任务队列的类型
任务队列存在两种类型，一种是microtask queue，一种是macrotask queue。
##### 任务队列的区别
* microtask queue: 唯一，整个事件循环中，仅存在一个；执行为同步，同一事件循环中的microtask会按队列顺序，串行执行完毕。(ES6中的promise和DOM3的MutationObserver)
* macrotask queue: 不唯一，存在一定的优先级(用户I/O部分优先级更高)；异步执行，同一事件循环中只执行一个。