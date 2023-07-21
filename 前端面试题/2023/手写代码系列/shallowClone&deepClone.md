### 浅拷贝
#### API实现
```js
1、Object.assign(target, source)
2、arr.slice(0)
```
#### 手写实现
```js
const shallowClone = source => {
  let target
  let type = Object.prototype.toString.call(source).slice(8, -1)
  if(type === 'Object'){
    target = {}
  }else if(type === 'Array'){
    target = []
  }
  for(prop in source){
    if(Object.prototype.hasOwnProperty.call(source, prop)){
      target[prop] = source[prop]
    }
  }
  return target
}
```
### 深拷贝
#### 递归实现
```js
const checkType = unknownData => Object.prototype.toString.call(unknownData).slice(8, -1)
const deepClone = source => {
  let target, sourceType = checkType(source)
  if(sourceType === 'Object'){
    target = {}
  }else if(sourceType === 'Array'){
    target = []
  }
  for(let prop in source){
    if(Object.prototype.hasOwnProperty.call(source, prop)){
      let data = source[prop]
      let dataType = checkType(data)
      if(dataType === 'Object' || dataType === 'Array'){
        target[prop] = deepClone(source[prop]
      }else{
        target[prop] = source[prop]
      }
    }
  }
  return target
}
```
但是这个过程中还需要考虑到另外的问题：
1、参数检查：ES6引入的Set、Map、weakMap、weakSet
2、循环引用
3、同级引用
4、爆栈
```js
// 通过字典进行循环检测
const checkType = unknownData => Object.prototype.toString.call(unknownData).slice(8, -1)
const deepClone = (source, map = new Map()) => {
  if(map.has(source)){
    return map.get(source)
  }
  let target, sourceType = checkType(source)
  if(sourceType === 'Object'){
    target = {}
  }else if(sourceType === 'Array'){
    target = []
  }
  map.set(source, target)
  for(let prop in source){
    if(Object.prototype.hasOwnProperty.call(source, prop)){
      let data = source[prop]
      let dataType = checkType(data)
      if(dataType === 'Object' || dataType === 'Array'){
        target[prop] = deepClone(source[prop], map)
      }else{
        target[prop] = source[prop]
      }
    }
  }
  return target
}
```

```js
// 使用weakMap和while进行性能优化
const checkType = unknownData => Object.prototype.toString.call(unknownData).slice(8, -1)
const foreach = (array, cb){
  let index = -1
  const len = array.length
  while(++index < len){
    cb(array[index], index)
  }
}
const deepClone = (source, map = new weakMap()) => {
  if(map.has(source)){
    return map.get(source)
  }
  let target, keys, sourceType = checkType(source)
  if(sourceType === 'Object'){
    target = {}
    keys = Object.keys(source)
  }else if(sourceType === 'Array'){
    target = []
    keys = source
  }
  map.set(source, target)
  foreach(keys || source, (value, key) => {
    if(keys){
      key = value
    }
    if(dataType === 'Object' || dataType === 'Array'){
        target[key] = deepClone(source[key], map)
      }else{
        target[key] = source[key]
      }
  })
  return target
}
```

```js
// 解决爆栈问题（参数判断仅处理对象与数组）
const checkType = unknownData => Object.prototype.toString.call(unknownData).slice(8, -1)
const getInitValue = type => {
  if(type === 'Object'){
    return {}
  }else if(type === 'Array'){
    return []
  }
}
const foreach = (array, cb) => {
  let index = -1
  const len = array.length
  while(++index < len){
    cb(array[index], index)
  }
}
const deepClone = (source) => {
  const sourceType = checkType(source)
  const map = new weakMap()
  let root = getInitValue(sourceType)
  const loopList = [
    {
      parent: root,
      key: undefined,
      data: source
    }
  ]
  while(loopList.length > 0){
    const node = loopList.pop()
    const { parent, key, data } = node
    let res = parent
    if(typeof key !== 'undefined'){
      res = parent[key] = getInitValue(sourceType)
    }
    if(map.has(data)){
      parent[key] = map.get(data)
      continue
    }
    map.set(data, res)
    let keys
    if(sourceType === 'Object'){
      keys = Object.keys(data)
    }else if(sourceType === 'Array'){
      return undefined
    }
    foreach(keys || data, (value, key) => {
      if(keys){
        key = value
      }
      if(checkType(data[key]) === 'Object' || checkType(data[key]) === 'Array'){
        loopList.push({
          parent: res,
          key,
          data: data[key]
        })
      }else{
        res[key] = data[key]
      }
    })
  }
  return root
}
```