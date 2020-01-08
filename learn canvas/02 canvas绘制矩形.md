### 绘制矩形

> canvas提供了三种方法绘制矩形

> 1. `fillRect(x,y,width,height)` 绘制一个实心矩形
> 2. `strokeRect(x,y,width,height)` 绘制一个空心的边框
> 3. `clearRect(x,y,width,height)` 清除指定矩形区域，让清除部分完全透明

> x,y是矩形左上角的坐标；width，height矩形的宽高
>
> 注：上面的`fillRect`相当于是把构思图形参数和下笔作画融于一处，这样可以减少步骤

##### 01. 绘制一个实心矩形

```html
<body>
    <canvas width="500" height="500">如果浏览器版本过低，则此处文字会显示出来</canvas>
    <script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        canCon.fillStyle = "red"; //canCon.fill拿起canvas画笔，style是画笔的颜色
        canCon.fillRect(200, 200, 100, 100)
    </script>
</body>
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107184425250.png" alt="image-20200107184425250" style="zoom:50%;" />

##### 02. 空心矩形

```js
 let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        canCon.strokeStyle = "red"; //拿起画空心的笔，蘸上红色的墨
        canCon.strokeRect(200, 200, 100, 100)
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107184838079.png" alt="image-20200107184838079" style="zoom:50%;" />

##### 03. 清除指定区域

```js
 let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        canCon.fillStyle = "red"; //canCon.fill拿起canvas画笔，style是画笔的颜色
        canCon.fillRect(200, 200, 100, 100)
        canCon.clearRect(225, 225, 50, 50)
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107185408694.png" alt="image-20200107185408694" style="zoom:50%;" />