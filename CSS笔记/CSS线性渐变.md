### 线性渐变
#### 水平等宽条纹
```
background: linear-gradient(#fb3 50%, #58a 50%)
```
#### 垂直等宽条纹
```
background: linear-gradient(to right /* 90deg */, #fb3 50%, #58a 0)
background-size: 30px 100%
```
#### 斜条纹
```
background: linear-gradient(45deg, #fb3 25%, #58a 0, #58a 50%, #fb3 0, #fb3 75%, #58a 0);
background-size: 30px 30px;
/* 更好的方法 */
background: repeating-linear-gradient(45deg, #fb3, #fb3 15px, #58a 0, #58a 30px);

background: repeating-linear-gradient(45deg, #fb3 0 15px, #58a 15px 30px);

/* 也可以使用背景色加设置间隔颜色实现 */
background: #58a;
background-image: repeating-linear-gradient(45deg, hsla(0, 0%, 100%, .1), hsla(0, 0%, 100%, .1) 15px, transparent 0, transparent 30px);
```
### 径向渐变
#### 波点
```
background: #655;
background-image: radial-gradient(tan 30%, transparent 0),
radial-gradient(tan 30%, tansparent 0);
background-size: 30px 30px;
background-position: 0 0, 15px 15px;
```