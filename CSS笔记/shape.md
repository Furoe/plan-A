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
@mixin polygn(){
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