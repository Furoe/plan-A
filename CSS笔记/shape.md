### 变形
#### 圆以及椭圆
> 本质上是以水平半径和垂直半径实现圆和椭圆效果 

```scss
@mixin circle(){
  border-radius: 50%;
}
@mixin quatorCircle(){
  border-radius: 100% 0 0 0;
}
@mixin ellipse(){
  border-radius: 100% / 50%;
}
```
#### 平行四边形
```scss
@mixin parallelogram(){
  transform: skewX(-45deg);
}
```
#### 菱形
```scss
// 菱形
@mixin polygon(){
  clip-path: 50% 0, 100% 50%, 50% 100%, 0 50%; 
}
//悬浮恢复
img{
  clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
  transition: 1s clip-path;
}
img:hover{
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}
```
#### 梯形
```scss
.trapzoid{
  position: relative;
  display: inline-block;
  padding: .5em 1em 0.35em;
}
.trapzoid::before{
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  background: #58a;
  transform: scaleY(1.3) perspective(.5em) rotateX(5deg);
  transform-origin: bottom;
}
```