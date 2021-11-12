### 线性渐变
#### 水平等宽条纹
```scss
.style{
  background: linear-gradient(#fb3 50%, #58a 50%);
}
```
#### 垂直等宽条纹
```scss
.style{
  background: linear-gradient(to right /* 90deg */, #fb3 50%, #58a 0);
  background-size: 30px 100%;
}
```
#### 斜条纹
```scss
.style1{
  background: linear-gradient(45deg, #fb3 25%, #58a 0, #58a 50%, #fb3 0, #fb3 75%, #58a 0);
  background-size: 30px 30px;
}
/* 更好的方法 */
.style2{
  background: repeating-linear-gradient(45deg, #fb3, #fb3 15px, #58a 0, #58a 30px);
}

.style3{
  background: repeating-linear-gradient(45deg, #fb3 0 15px, #58a 15px 30px);
}

/* 也可以使用背景色加设置间隔颜色实现 */
.style4{
  background: #58a;
  background-image: repeating-linear-gradient(45deg, hsla(0, 0%, 100%, .1), hsla(0, 0%, 100%, .1) 15px, transparent 0, transparent 30px);
}
```
### 径向渐变
#### 波点
```scss
.polka{
  background: #655;
  background-image: radial-gradient(tan 30%, transparent 0),
  radial-gradient(tan 30%, transparent 0);
  background-size: 30px 30px;
  background-position: 0 0, 15px 15px;
}
```
#### 棋盘
```scss
@mixin chessBoard($base, $accent, $size){
  background: $base;
  background-image: linear-gradient(45deg, $base 25%, transparent 0, transparent 75%, $base 0),
                    linear-gradient(45deg, $base 25%, transparent 0, transparent 75%, $base 0);
  background-position: 0, 0, $size, $size;
  background-size: 2*$size 2*$size;
}
@include chessBoard(#eee, #bbb, 15px)
```
### 角向径变
```scss
// 色轮
.linear-circle{
  background: conic-gradient(red, yellow, lime, aqua, blue, fuchsia, red);
}

.chessBoard{
  background: repeating-conic-gradient(#bbb 0, #bbb 25%, #eee 0, #eee 50%);
  background-size: 30px 30px;
}
```