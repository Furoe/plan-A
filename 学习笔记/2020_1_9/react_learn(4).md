##### 
React 组件可以通过数组的形式返回多个元素。
```
render(){
	return (){
		[
			<li key='A'>First Item</li>,
			<li key='B'>Second Item</li>，
			<li key='C'>Third Item</li>,
		]
	}
}
```