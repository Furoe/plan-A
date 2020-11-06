#### vuex-router-sync
将vue-router状态放进state中。
```
//同步的属性
{
	path: '',
	query: null,
	params: null
}
```
##### 安装
```
npm install vuex-router-sync --save
```
##### 使用
```
import { sync } from 'vuex-router-sync'
sync(store, router)
```