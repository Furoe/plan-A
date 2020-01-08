#### 事件处理
JSX类的方法默认是不会绑定this的。
```
this.handleClick = this.handleClick.bind(this);
<button onClick={this.handleClick}></button>

or

<button onClick={(e) => this.handleClick(e)></button>

or

//实验性语法，属性初始化器
handleClick = () => {
	console.log();
}
```
使用箭头函数的方法有一个缺点，每次LoggingButton渲染的时候都会创建一个不同回调函数，
当回调函数作为参数传递给低阶组件的时候，会造成额外的重新渲染。
#### 事件传参
```
<button onClick={(e) => this.handleClick(id, e)}></button>
<button onClick={this.handleClick.bind(this, id)}></button>
```
通过bind函数像监听函数传参，在类组件中定义的监听函数，事件对象e要放在参数后面。
#### 状态提升
组件共用状态数据时，将共享的状态提升到最近的父组件。