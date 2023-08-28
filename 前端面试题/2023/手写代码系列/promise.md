### promise
1、Promise只有三种状态，`pending`、`fulfilled`和`rejected`。
```js
const PENDING = 'pending'
const FULFILLED = 'fulfilled'
const REJECTED = 'rejected'

function resolvePromise(promise, value, resolve, reject){
  if(promise === value){
    return reject(new TypeError('Chaining cycle detected for promise'))
  }
  let called = false
  if(value !== null && (typeof value === 'object' || typeof value === 'function')){
    try{
      let then = value.then
      if(typeof then === 'function'){
        then.call(value, res => {
          if(called) return
          called = true
          resolvePromise(promise, res, resolve, reject)
        }, err => {
          if(called) return
          called = true
          reject(err)
        })
      }else{
        called = true
        resolve(value)
      }
    }catch(e){
      if(called) return
      called = true
      reject(e)
    }
  }else{
    resolve(value)
  }
}

class myPromise {
  constructor(fn){
    this.state = PENDING
    this.value = undefined
    this.reason = undefined
    this.onResolvedCallbacks = []
    this.onRejectedCallbacks = []
    let resolve = value => {
      if(this.state === 'pending'){
        this.state = FULFILLED
        this.value = value
        this.onResolvedCallbacks.map(cb => cb())
      }
    }
    let reject = value => {
      if(this.state === 'pending'){
        this.state = REJECTED
        this.reason = value
        this.onRejectedCallbacks.map(cb => cb())
      }
    }

    try{
      fn(resolve, reject)
    }catch(err){
      reject(err)
    }
  }
  then(onFulfilled, onRejected){
    let newPromise = new myPromise((resolve, reject) => {
      if(this.state === FULFILLED){
        let res = onFulfilled(this.value)
        resolvePromise(newPromise, res, resolve, reject)
      }
      if(this.state === REJECTED){
        let res = onRejected(this.reason)
        resolvePromise(newPromise, res, resolve, reject)
      }
      if(this.state === PENDING){
        this.onResolvedCallbacks.push(() => {
          let res = onFulfilled(this.value)
          resolvePromise(newPromise, res, resolve, reject)
        })
        this.onRejectedCallbacks.push(() => {
          let res = onRejected(this.reason)
          resolvePromise(newPromise, res, resolve, reject)
        })
      }
    })
    return newPromise 
  }
}

// Promise.resolve
myPromise.resolve = function(val){
  return new myPromise((resolve, reject) => {
    resolve(val)
  })
}

// promise.reject
myPromise.reject = function(val){
  return new myPromise((resolve, reject) => {
    reject(val)
  })
}

// Promise.all
myPromise.all = function(arr){
  return new myPromise((resolve, reject) => {
    let result = []
    let i = 0, len = arr.length
    for(;i < len;i++){
      arr[i].then(res => {
        result[i++] = res
        if(i === len) {
          resolve(result)
        }
      }).catch(err => {
        throw new Error(err)
      })
    }
  })
}

// Promise.race
myPromise.race = function(arr){
  return new myPromise((resolve, reject) => {
    let len = arr.length
    for(let i = 0;i < len;i++){
      arr[i].then(res => {
        return resolve(res)
      }).catch(err => {
        throw new Error(err)
      })
    }
  })
}

```
#### 应用
##### 异步并发数控制
```js
class schedule{
  constructor(maxNum){
    this.maxNum = maxNum
    this.count = 0
    this.taskList = []
  }
  add(promiseCreator){
    if(this.count >= maxNum){
      await new Promise((resolve) => {
        this.taskList.push(resolve)
      })
    }
    this.count++
    let res = await promiseCreator()
    this.count--
    if(this.taskList.length){
      this.taskList.shift()()
    }
    return res
  }
}
```