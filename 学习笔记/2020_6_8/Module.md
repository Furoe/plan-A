#### Module的加载模式
在ES6之前，有CommonJS和AMD两种模式，CommonJS主要服务于服务器端，
AMD服务于浏览器。
```JavaScript
let {stat, exists, readfile} = require('fs');
//实质是加载完整模块，生成一个对象，然后从这个对象上提取这三个方法
//这种加载称为"运行时加载"

//ES6
import {stat, exists, readfile} from 'fs';
//实质是从'fs'模块加载3个方法，其他方法不加载。
//这种加载称为"编译时加载"
```
#### 跨模块常量