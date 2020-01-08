### 01. 绘制弧线

> 弧线可不和圆弧一样，圆弧是标准圆上的一段。

> 方法：`arcTo(x1,y1,x2,y2,r)`
>
> 根据给定的控制点和半径画一段弧线，再以直线连接两个控制点
>
> 图解：
>
> ![image-20200108145238968](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108145238968.png)
> $$
> 最终显示弧线=线段ab+圆弧bc
> $$

> 画个弧线：

```js
 <script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        canCon.strokeStyle = "black"; 
        canCon.moveTo(150, 20);
        canCon.arcTo(150, 100, 50, 20, 20)
        canCon.stroke();
    </script>
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108144612427.png" alt="image-20200108144612427" style="zoom:50%;" />

### 02. 绘制贝塞尔曲线

##### 2.1贝塞尔曲线的由来

> - 其实贝塞尔曲线的数学基础最早是1912年就在当世广为人知的伯恩斯坦多项
> - 虽然在1912年就已经被发现，但是其对图形的适用性在半个世纪内者也没有被实现，直到1959年在雪铁龙汽车就职的数学家 Paul de Casteljau，开始对伯恩斯坦多项式进行图形化的尝试，并推出一种新的数值稳定(即在求伯恩斯坦多项式的时候不会引入数值误差)递归算法 de Casteljau 算法用来伯恩斯坦多项式。根据这个算法，就可以只通过很少的控制点，去生成复杂的平滑曲线，也就是贝塞尔曲线。
> - 而贝塞尔曲线的成名，得益于法国工程师 Pierre Bézier ，他将这种算法用来辅助雷诺汽车的车体工业设计，并且得到广泛宣传。

##### 2.2 如何绘制贝塞尔曲线

> 1. 画线段AC，BC, 相交于C点
> 2. 在线段AC取点D，BC上取点E使 AD:DC = CE:EB 。 如下图所示：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108150331893.png" alt="image-20200108150331893" style="zoom:100%;" />

> 3.连接点D、E
> 4.在线段DE上取点F，使 AD:DC = CE:EB = DF:FE。 如下图：

![image-20200108150444653](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108150444653.png)

> 那么我们就找到了贝塞尔曲线上的点F，这时让选取的点 D 在线段AB上从起点 A 移动到终点 B，找出所有的贝塞尔曲线上的点 F。**所有的点**找出来之后，我们也得到了这条贝塞尔曲线。如下图：

![image-20200108150532692](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108150532692.png)

> 如果你实在想象不出这个过程，没关系，看动画！

![](F:\前端开发\canvas学习\images\172968-82781ddb157c4c6a.webp)

##### 2.3 canvas绘制二次贝塞尔曲线

> - 二次贝塞尔曲线是一个控制一个结束点
> - `quadraticCurveTo()` 方法通过使用表示二次贝塞尔曲线的指定控制点，向当前路径添加一个点。
> - 方法：`quadraticCurveTo(cp1x,cp1y,x,y)`
> - 绘制二次贝塞尔曲线，cp1x,cp1y为一个控制点，x,y为结束点

> 绘制一条二次贝塞尔曲线：

```js
<script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        canCon.fillStyle = "black";
        canCon.beginPath();
        canCon.moveTo(150, 120);
        canCon.quadraticCurveTo(150, 180, 300, 120)
        canCon.stroke();
    </script>
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108151904866.png" alt="image-20200108151904866" style="zoom:50%;" />

##### 2.4 canvas绘制三次贝塞尔曲线

> 三次贝塞尔曲线是有两个控制点和一个结束点
>
> 方法：`bezierCurveTo(cp1x,cp1y,cp2x,cp2y,x,y)` 

> 画个三次贝塞尔曲线：

```js
 <script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        canCon.beginPath();
        canCon.moveTo(150, 20);
        canCon.bezierCurveTo(120, 100, 80, 100, 20, 20)
        canCon.stroke();
    </script>
```

实际效果：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108154017475.png" alt="image-20200108154017475" style="zoom:50%;" />

图解：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108154058152.png" alt="image-20200108154058152" style="zoom:50%;" />

