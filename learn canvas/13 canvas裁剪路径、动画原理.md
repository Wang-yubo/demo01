### 1. canvas裁剪路径

> 裁剪路径和普通的`canvas`图形差不多，不同的是它的作用是遮罩，用来隐藏不需要的部分。如下图所示，红边五角星就是裁切路径，所有在路径以外的部分都不会在`canvas`里面绘制出来

![](F:\Code\gitDemo\learn canvas\images\clipping_five_star.png)

> 方法：
>
> 1. `canCon.clip();`
> 2. `canCon.clip(fillRule);`
> 3. `canCon.clip(path,fillRule)`;将当前正在构建的路径转换为当前的裁剪路径
>
> - `canvas`使用`clip()`方法来创建一个新的裁切路径
> - 默认情况下，`canvas`有一个与他自身一样大的裁切路径（也就是没有裁切效果）
>
> `fillRule`：
>
> 1. 这个算法判断一个点是在路径内还是在路径外
> 2. 可选项：
>
> - `nonzero`：非零环绕原则，默认的原则
> - `evenodd`：奇偶环绕原则

> 来个奇偶环绕的例子：

```js
<script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        let path = new Path2D();
        path.arc(250, 250, 15, 0, Math.PI * 2);
        path.arc(250, 250, 30, 0, Math.PI * 2);
        path.arc(250, 250, 45, 0, Math.PI * 2);
        path.arc(250, 250, 60, 0, Math.PI * 2);
        path.arc(250, 250, 75, 0, Math.PI * 2);
        path.arc(250, 250, 90, 0, Math.PI * 2);
        canCon.fillStyle = "white";
        canCon.clip(path, 'evenodd');
        canCon.fillRect(0, 0, 500, 500)
    </script>
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110143410175.png" alt="image-20200110143410175" style="zoom:50%;" />

> 这是六个同心圆的情况，再加一个：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110143722783.png" alt="image-20200110143722783" style="zoom:50%;" />

> - 观察一下，6个同心圆的情况下，最里面一个是红色，最外面是白色，7个的时候，最里面一个是白色，最外面还是白色；
> - 分析一下，如果七个的时候也是按照6个的那种渲染方式（最里面是红色），那么第七个也是红色，这种情况下会融合进周围的背景色中看不出显示的效果，所以`evenodd`的奇偶环绕原则会避免这种情况，改变了渲染方式，让最外层也一定渲染出来。

### 2. canvas动画原理

##### 2.1 动画的基本要素：

> 1. 单位时间内连续播放多张图片。一般以秒为单位，刷新频率一般为60hz，为了保证流畅，一秒要播放大于等于60张图片。
> 2. 每张图片内的物体状态必须要发生改变

##### 2.2 普通动画

> 直接写个普通动画

```js
<script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        var y = 100 //给一个初始的圆心位置，接下来每次绘制的时候圆心的y的位置都往下移动一个距离
        setInterval(function() { //js里动画肯定要用定时器来实现了
            canCon.beginPath(); //每次作画之前都要把笔抬起来，否则会出现“连笔”的情况
            canCon.clearRect(0, 0, 500, 500); //每次画之前都要清除上一个，否则就图像就会堆叠起来
            canCon.fillStyle = 'red';
            canCon.arc(250, y++, 66, 0, Math.PI * 2);
            canCon.fill();
        }, 1000 / 60)
    </script>
```

![](F:\Code\gitDemo\learn canvas\images\普通动画.gif)

##### 2.3 长尾动画

> - 普通动画是利用`clearRect`函数清除前一帧动画。
> - 长尾动画是用一个半透明的`fillRect`函数，来欺骗视觉，到达效果

> 来个长尾动画：

```js
 <script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        ~~ function setSize() {
            window.onresize = arguments.callee;
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }();

        var y = 0;
        setInterval(function() { //js里动画肯定要用定时器来实现了
            canCon.beginPath(); //每次作画之前都要把笔抬起来，否则会出现“连笔”的情况
            canCon.fillStyle = 'rgba(0,0,0,0.1)'
            canCon.fillRect(0, 0, canvas.width, canvas.height)
            canCon.fillStyle = '#fff';
            canCon.fillRect(500, y++, 2, 10);
            canCon.fill();
        }, 1000 / 60)
    </script>
```

<img src="F:\Code\gitDemo\learn canvas\images\长尾动画.gif" style="zoom:50%;" />

