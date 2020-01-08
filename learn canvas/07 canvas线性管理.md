### 01. 线性管理基本参数

| 属性                     | 说明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| `lineWidth = value`      | 设置线条宽度                                                 |
| `lineCap = type`         | 设置线条末端样式                                             |
| `lineJoin = type`        | 设定线条与线条之间结合处的样式                               |
| `miterLimit = value`     | 限制当两条线相交时交界处最大长度<br />所谓交接长度是指线条交接处内角顶点到外角顶点长度的长度 |
| `getLineDash`            | 返回一个包含当前虚线样式，长度为非负偶数的数组               |
| `setLineDash(segments)`  | 设置当前虚线样式                                             |
| `lineDashoffset = value` | 设置虚线样式的起始偏移量                                     |

##### 1.1 `lineWidth`

```js
lineWidth = "value";
```

> 这个属性设置当前绘线的粗细，属性必须为正数

> 用递增的宽度绘制10条线：

```js
 <script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        function creatLine(num) {
            for (var i = 0; i < num; i++) {
                canCon.lineWidth = 1 + i
                canCon.beginPath();
                canCon.moveTo(5 + i * 14, 5)
                canCon.lineTo(5 + i * 14, 140)
                canCon.stroke()
            }
        }
        creatLine(10)
    </script>
```

> 查看效果：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108192446122.png" alt="image-20200108192446122" style="zoom:50%;" />

> 精确测量一下：

![image-20200108192523264](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108192523264.png)

> 按照设计，线宽应该是从1到10，++1，可是实际情况并没有出现奇数

> 原理探究
>
> 第一点：线宽是什么
>
> - 线宽是指给定路径的中心到两边的粗细。换句话说就是在路径的两边各绘制线宽的一半。因为画布的坐标并不和像素直接对应，当需要获得精确的水平或者垂直线的时候要特别注意（毕竟屏幕的最小单位为1，没法搞成0.5px）
>
> 从图中可以看出某些线的两边有明显的明暗变化，暗的部分就是`canvas`和显示器自动调整的，所以`canvas`是通过调整显示器的着色色调来欺骗视觉，让实际效果看起来像是有奇数宽度一样。

> 第二点：网格和坐标
>
> 用网格来代表canvas的坐标格子，每一个对应屏幕上的一个像素点。在第一个图中，填充了（2,1）至（5,5）的矩形，整个区域的边界刚好落在像素边缘上，这样得到的矩形有清晰地边缘，所以，`canvas`可以精确得画出矩形

![image-20200108195719872](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108195719872.png)

> - 如果逍遥绘制出一条从（3,1）到（3.5），宽度是1.0的线条，你就会得到像图2一样的结果。实际填充区域（深蓝色部分），仅仅延伸至路径两旁各一半像素。而这半个像素又以近似的方式进行渲染，这意味着那些像素只是部分着色，结果就以实际笔触颜色一半色调的颜色来填充整个区域（浅蓝和深蓝的部分）
> - 要解决这个问题，就必须对路径施以更加精确的控制。像第三幅一样绘制从（3.5,1）到（3.5,5）的线条，其边缘正好落在边界，填充出来就是准确的宽为1.0的线条

##### 1.2 lineCap

```js
lineCap = "butt"；
lineCap = "round"；
lineCap = "square"；
```

> - 属性`lineCap`的值决定了线段端点显示的样式，它有三个可选项`butt`，`round`和`square`
> - 默认为`butt`

![image-20200108202459246](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108202459246.png)

> - 中间的是`round`，半径为一半线宽的半圆
> - 最右边的是`square`，等宽且高度为一半线宽
> - 可以看得出`square`和butt在样式上完全一样，都是方的，只不过`square`比`butt`长了一点。

##### 1.3 lineJoin 

```js
lineJoin = "round";
lineJoin = "bevel";
lineJoin = "miter";
```

> - lineJoin的属性值决定了图形中两线段连接处所显示的样子
> - 它可以是以上三种之一
> - 默认为miter

![image-20200108203612754](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108203612754.png)

> - 最上面一条是round的效果，边角处被磨圆了，圆的半径等于线宽
> - 中间一条是bevel，连接出是平的
> - 最下面一条是miter，连接处是尖的

##### 1.4 虚线设置

> - 用setLineDash方法和lineDashOffset属性来制定虚线样式
>
> - setLineDash方法接受一个数组，来指定线段与间隙的交替
>
>   ```js
>    canCon.setLineDash([4, 2])
>   ```
>
>   指定线段长度为4，间隔为2
>
> - lineDashOffset属性设置起始

> 来一个流动的虚线：

```js
 <script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        var offset = 0;
        function draw() {
            canCon.clearRect(0, 0, canvas.width, canvas.height);
            canCon.setLineDash([4, 2]);//
            canCon.lineDashOffset = -offset;//+号向右移动，-号向左移动
            canCon.strokeRect(10, 10, 100, 100)
        }
        function march() {
            offset++;
            if (offset > 12) {//ofset一般为[4, 2]这个数组之和的整数倍，这样看起来才流畅
                offset = 0;
            }
            draw();
            setTimeout(march, 20)
        }
        march();
    </script>
```

> 实际效果：

![](F:\Code\gitDemo\learn canvas\images\流动的虚线.gif)

> 改成不是整数倍，来个卡顿效果：

![](F:\Code\gitDemo\learn canvas\images\卡顿.gif)



