#### Sass
sass根据语法分为两种格式Sass和Scss。  
scss与css更类似，有大括号，文件后缀是.scss。   
sass使用缩进来表示关系，文件后缀是.sass。  
##### 变量
变量以$开头，用来存储重复使用的数据，包括宽度、高度和颜色等等。 
如果变量需要嵌在字符串中，则需要写在`#{}`中。  
但是如果变量是数字要避免`#{$value}px`这种写法，尽量使用`$value * 1px`。
```SCSS
$side: left;
.rounded {
	border-#{$side}-radius: 5px;
}
```  
###### 全局变量与局部变量
定义在顶层的是全局变量，定义在块中的是局部变量，局部变量可以跟全局变量重名。  
```SCSS
$global-variable: global value;
.content {
	$local-variable: local value;
	global: $global-variable;
	local: $local-variable;
}
```  
如果需要在局部环境声明一个全局变量，使用!global标志。
```SCSS
$variable: first global value;
.content {
	$variable: second global value !global;
	value: $variable;  //second global value;
}

.sidebar {
	value: $variable;  // second global value
}
```
##### 嵌套
```SCSS
nav{
	.ul{
		margin: 0
	}
}

//css
nav ul{
	margin: 0
}
```
在嵌套的代码块中，可以引用父级元素。
```SCSS
a {
	&:hover {
		color: #ffb3ff;
	}
}
```
##### 模块
不需要将所有sass写在同一个文件中，可以根据功能或者意义分割成模块。
然后使用`@use`引入模块。当前只有Dart Sass支持`@use`，其他使用`@import`。
```SCSS
//_base.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body{
	font: 100% $font-stack;
	color: $primary-color;
}

//style.scss
@use 'base';
.inverse {
	background-color: base.$primary-color;
	color: white;
}
```
##### 混入
在考虑浏览器兼容性的时候，有很多属性需要重复写，这时候使用混入，用混入
的方式写兼容性语句，只需要考虑样式的值，不需要重复的书写。
```SCSS
@mixin transfrom($property) {
	-webkit-transform: $property;
	-moz-transform: $property;
	transform: $property;
}

.box{ @include tansform(rorate(30deg)); }
```
##### 继承
当一个基本样式不变的组件有多种样式，使用继承的方式可以减少重复代码。
```SCSS
%message-shared {
	border: 1px solid #ccc;
	padding: 10px;
	color: #333;
}

%message-heights {
	display: flex;
	flex-wrap: wrap;
}

.message{
	@extend %message-shared;
}

.sucess {
	@extend %message-shared;
	border: green;
}

.error {
	@extend %message-shared;
	border: red;
}
```
##### 操作符
sass支持一些标准的数学运算符，比如+、-、*、/和%。  
```SCSS
.container {
	width: 100%;
}

article[role='main'] {
	float: left;
	width: 600px / 960px * 100%;
}

aside[role='complementary'] {
	float: left;
	width: 300px / 960px * 100%;
}
```  
##### 注释
标准的注释/* comment */，会保留到编译后的文件。  
单行注释// comment，只保留在源文件中，编译后被省略。  
在/*后加上!，表示这是重要注释。即使是压缩模式编译，也会保留这行注释，通常  
可以用于声明版权信息。  
```
/*!
    important comment
*/
```
##### 高级用法
###### 条件语句
`@if`和`@else`
```SCSS
p {
	@if 1 + 1 === 2 { border: 1px solid; }
	@else { border: 2px dotted; }
}
```
###### 循环语句
```SCSS
//for循环
@for $i from 1 to 10 {
	.border-#{$i} {
		border: $i * 1px solid blue;
	}
}

//while循环
$i: 6;
@while $i > 0 {
	.item-#{$i} {
		width: 2em * $i;
		$i: $i - 2;
	}
}

//each
@each $member in a, b, c, d {
	.#{member} {
		background-image: url('/image/#{member}.jpg');
	}
}
```
###### 自定义函数
```SCSS
@function double($n) {
	@return $n * 2;
}

#sider {
	width: double(5px);
}
```
##### 内置函数
###### 颜色函数
```SCSS
lighten(#cc3, 10%)  //#d6d65c
darken(#cc3, 10%)  //#a3a329
grayscale(#cc3)  //#808080
complement(#cc3) //#33c
```