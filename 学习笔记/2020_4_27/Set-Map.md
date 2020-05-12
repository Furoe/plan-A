#### Set
``` JavaScript
//去除数组重复元素
[...new Set(Array)];

//去除字符串重复字符
[...new Set('ababc')].join('');
```
##### Set实例的属性和方法
- `Set.prototype.constructor`:构造函数，默认是`Set`函数
- `Set.prototype.size`:返回`Set`实例额成员总数
- `Set.prototype.add()`
- `Set.prototype.delete`
- `Set.prototype.has()`
- `Set.prototype.clear()`

##### Set遍历操作
- `Set.prototype.keys()`: 返回键名的遍历器
- `Set.prototype.values()`: 返回键值得遍历器
- `Set.prototype.entries()`: 返回键值对的遍历器
- `Set.prototype.forEach()`: 使用回调函数遍历每个成员

#### WeakSet
WeakSet成员只能是对象，不能是其他类型的值。
WeakSet中成员都是弱引用，垃圾回收机制不考虑WeakSet对该对象的引用，WeakSet不可遍历。
#### Map
##### 对象转Map
```
let obj = {'a': 1, 'b': 2};
let map = new Map(Object.entries(obj));
```
##### Map转JSON
键名都是字符串，转为对象JSON
map=>obj=>JSON
键名有非字符串，转为数组JSON
```JavaScript
JSON.stringify([...map])
```
##### JSON转Map
键名全为字符串
objToMap(JSON.parse(str))
键名有非字符串
new Map(JSON.parse(str))