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
##### 布尔值、null和undefined被忽略
```
<div></div>
<div>{true}</div>
<div>{false}</div>
<div>{null}</div>
<div>{undefined}</div>
```
实际应用可以用来控制组件的显示
```
<div>
	{showHeader && <Header />}  //只有showHeader为true才会渲染<Header />组件
</div>
```