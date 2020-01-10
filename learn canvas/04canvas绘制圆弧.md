### 绘制圆弧

> - 绘制圆弧或者圆，使用`arc()`方法，不过它的实现不可靠
> - `arc(x,y,r,startAngle,endAngle,anticlockwise)`
> - x,y为绘制圆弧所在圆上的圆心坐标
> - r为半径
> - `startAngle`，`endAngle`为开始弧度和结束弧度
> - `anticlockwise`为逆时针方向，默认为true逆时针方向，false为顺时针方向

> 注意：arc()函数中的表示角的单位是弧度，而不是角度
>
> 角度与弧度换算公式：

$$
弧度=（Math.PI/180）*deg
$$

> 画个弧线

```js
 <script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        canCon.moveTo(250, 250);
        canCon.arc(250, 250, 50, 0, Math.PI, true)
        canCon.stroke()
    </script>
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107195814775.png" alt="image-20200107195814775" style="zoom:50%;" />

> - 可以看到位置1处并非我们想要的。
> - 这是因为起始点和圆弧开始的位置不一致导致`canvas`自动补全产生的
>
> 调整起始点到圆弧开始位置后：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107200110932.png" alt="image-20200107200110932" style="zoom:50%;" />

> 再画个弧度大点的：

```js
 canCon.arc(250, 250, 50, 0, Math.PI / 2, true)
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107200443477.png" alt="image-20200107200443477" style="zoom:50%;" />

> 再画个弧度更大的：

```js
 canCon.arc(250, 250, 50, 0, Math.PI / 8, true)
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107200549809.png" alt="image-20200107200549809" style="zoom:50%;" />

> 可以看出，在第六个参数为true的前提下：当第五个参数为`Math.PI`时，画出了半圆的弧线，当第五个参数为`Math.PI/2`时，画出了半圆的弧线画出了3/4个圆的弧线，当第五个参数为`Math.PI/8`时，画出了半圆的弧线画出了7/8个圆的弧线。
>
> 总结，此时第五个参数越小，弧度越大。
>
> 来个示意图：
>
> ![](F:\Code\gitDemo\learn canvas\images\圆弧.jpg)

> 把true改成false后
>
> `Math.PI/8`时：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107201207116.png" alt="image-20200107201207116" style="zoom:50%;" />

> `Math.PI/2`时

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107201302573.png" alt="image-20200107201302573" style="zoom:50%;" />

> `Math.PI`时

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107201341271.png" alt="image-20200107201341271" style="zoom:50%;" />

> 到底用true还是false还是按实际方向来

