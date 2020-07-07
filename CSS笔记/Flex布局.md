#### Flex布局
行内元素也可以使用弹性布局
```
.box{
	display: inline-flex;
}
```
Attention: 设为flex布局后，子元素的`float`、`clear`和`vertical-align`将失效。
##### flex-direction
决定主轴的方向
```
.body{
	flex-direction: row | column | row-reverse | column-reverse
}
```
#### flex-wrap
控制换行
```
.body{
	flex-wrap: nowrap | wrap | wrap-reverse
}
```
wrap-reverse: 换行，第一行在下方
#### flex-flow
`flex-flow`是`flex-direction`和`flex-wrap`的简写形式，默认值为`row nowrap`。
```
.body{
	flex-flow: <flex-direction> || <flex-wrap>
}
```
#### justify-content
决定项目在主轴上的对齐方式
```
.box{
	justify-content: flex-start | flex-end | center | space-between | space-arround
}
```
#### align-items
```
.box{
	aligin-items: flex-start | flex-end | center | baseline | stretch
}
```
#### align-content
定义多根轴线的对齐方式，一条轴线不起作用。
```
.box{
	aligin-content: flex-start | flex-end | space-between | space-around | stretch
}
```
#### order
元素属性，定义元素的排列顺序，数值越小越靠前，默认为0。
```
.item{
	order: <integer>
}
```
#### flex-grow
元素的放大比例，默认为0。
```
.item{
	flex-grow: <number>
}
```
#### flex-shrink
元素的缩小比例，默认为1。
```
.item{
	flex-shrink: <number>
}
```
#### flex-basis
定义在分配多余空间之前，项目占的主轴空间。默认值`auto`，即项目的原本大小。
.item{
	flex-basis: <length> | auto
}
#### flex
`flex`是`flex-grow`、`flex-shrink`和`flex-basis`的简写。
#### align-self
`align-self`允许元素有与其它元素不一样的对齐方式，可覆盖`align-items`属性，默认`auto`。
表示继承父元素的`align-items`，如果没有父元素，则是`stretch`。
```
.item{
	align-self: auto | flex-start | flex-end | baseline | stretch
}
```