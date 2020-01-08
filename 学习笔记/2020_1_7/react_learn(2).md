#### React
React的核心思想就是封装组件，组件维护自己的状态和UI，当组件状态改变时，自动渲染整个组件。
* 组件
* JSX
* virtual DOM
* Data Flow
##### 组件
```
import React from 'react';
import {render} from 'react-dom';

class HelloMessage extends React.Component{
	render(){
		return (
			<div>hello, {this.props.name}</div>
		);
    }
}

render(<HelloMessage name='John' />, mountNode);
```
##### JSX
React DOM在渲染之前默认会过滤所传入的值，所有内容渲染前会被转换成字符串，这样可以有效防止XSS攻击。
##### 组件
组件可以函数式定义，也可以采用ES6 class来定义。
```
function Welcome(props){
	return <h1>hello, {props.name}</h1>;
}

class Welcome extends React.Component{
	render(){
		return <h1>hello, {props.name}</h1>;
	}
}
```
###### 组件渲染
当react碰到用户自定义组件的时候，会将jsx属性作为单个对象传给组件。
```
function Welcome(props){
	return <h1>hello, {props.name}</h1>;
}

const ele = <Welcome name='Sara' />;
ReactDom.render(
	ele, 
	document.getElementById('root')
);
```
###### 组合组件
attention: 组件的返回值只能有一个根元素。
```
function Welcome(props){
	return <h1>hello, {props.name}</h1>;
}

function App(){
	return (
		<div>
			<Welcome name='Sara' />
			<Welcome name='John' />
			<Welcome name='Cahal' />
		</div>
	);
}

ReactDom.render(
	<App />,
	document.getElementById('root');
);
```
##### State和生命周期
只有类定义的组件能使用局部状态和生命周期钩子。
###### 状态更新可能是异步的
React可以将多个setState()调用合并成一个调用来提高性能。因为`this.props`和`this.state`可能是异步更新的，
不能依赖他们的值来计算下一状态。
```
//Wrong
this.setState({
	counter: this.state.counter + this.props.increment,
});

//Correct
this.setState((prevState, props) => {
	counter: prevState.counter + props.increment
});

//Correct
this.setState(function(prevState, props){
	return {
		counter: prevState.counter + props.increment
	};
});
```
##### named-export VS default-export
编译的时候碰到的问题
###### Named Export(`export`)
一个文件可以有多个命名导出，导入的时候需要用大括号包住。
```
import { MyClass, MyOtherClass } from "./MyClass";
```
###### Default Export(`export default`)
一个文件只能有一个默认导出。
```
import MyDefaultExport from "./MyFileWithADefaultExport";
```
