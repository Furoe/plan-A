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
#### 折角
```scss
.inflection-angle{
  background: #58a;
  background: linear-gradient(to right bottom, transparent 50%, rgba(0, 0, 0, .4) 0) no-repeat 100% 0 / 2em 2em,
              linear-gradient(-135deg, transparent 1.5em, rgba(0, 0, 0, .4));
}

@mixin folded-corner($background, $size, $angle: 30deg){
  position: relative;
  background: $background;
  background: linear-gradient($angle - 180deg, transparent $size, #background 0);
  border-radius: .5em;
  $y: $size / sin($angle);
  $x: $size / cos($angle);
  &::before{
    content: '';
    position: absolute;
    background: linear-gradient(to left bottom, transparent 50%, rgba(0, 0, 0, .2) 0, rgba(0, 0, 0, .4) 100% 0 no-repeat);
    width: $x;
    height: $y;
    transform: translateY($y - $x) rotate(2*$angle - 90deg);
    transform-origin: bottom right;
    border-bottom-left-radius: inherit;
    box-shadow: -.2em .2em .3em -.1em rgba(0, 0, 0, .2);
  }
}
.node{
  @include folded-corner(#58a, 2em, 40deg);
}
```