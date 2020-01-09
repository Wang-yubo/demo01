### 1. canvas状态保存

> - `save()` >>>保存画布(`canvas`)的所有状态
> - `restore()` >>>返回最近的状态，两个方法都没有参数。
> - `canvas`的状态就是当前画面应用的所有样式和变形的一个快照。
> - `canvas`状态存储在栈中，每当`save()`方法被调用后，当前的状态就被推送到栈中保存。
>
> 能够保存的状态包括：
>
> 1. 当前应用的变形(即移动，旋转和缩放)
> 2. `strokeStyle，fillStyle,globalAlpha,lineWidth,lineCap,lineJoin,miterLimit,shadowOffsetX,shadowOffsetY,shadowBlur,shadowColor,globalCompositeOperation`的值
> 3. 当前的裁切路径(`clipping path`)，下节介绍
>
> 可以调用任意多次`save`方法，每调用一次restore方法，上一个保存的状态就从栈中弹出，所有设定都恢复

> 来个小栗子：

```js
 <script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        canCon.fillRect(0, 0, 150, 150); //使用默认设置绘制一个矩形
        canCon.save(); //保存默认状态

        canCon.fillStyle = "#fff"; //在原有的配置基础上对颜色做改变
        canCon.fillRect(15, 15, 120, 120); //使用新的设置绘制一个矩形

        canCon.save(); //保存当前状态
        canCon.fillStyle = 'black'; //再次改变颜色配置
        canCon.globalAlpha = 0.5; //加个透明度
        canCon.fillRect(30, 30, 90, 90); //使用新配置绘制一个矩形

        canCon.restore(); //重新加载之前的颜色状态
        canCon.fillRect(45, 45, 60, 60); //使用上一次的配置绘制一个矩形

        canCon.restore(); //加载上上次的配置颜色设置
        canCon.fillRect(60, 60, 30, 30) //使用加载的配置绘制一个矩形
    </script>
```

> 看效果：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200109191526632.png" alt="image-20200109191526632" style="zoom:50%;" />

### 2. 变形

##### 2.1 移动`translate`

> `translate`方法，它用来移动`canvas`和它的原点到一个不同的位置
>
> `transl(x,y)`>>>该方法接收两个参数，x是左右偏移量，y是上下偏移量。

> 将上面的结果移动一下

```js
canCon.translate(150, 150);
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200109192239640.png" alt="image-20200109192239640" style="zoom:50%;" />

> 注意：`translate`移动的是坐标系，坐标系移动之后，后续的所有坐标均基于新的坐标系来计算。
>
> `translate`会被`save()`方法保存

##### 2.2 旋转 rotating

> - `rotate()`方法，它用于以原点为中心旋转`canvas`
> - `rotate(angle)`>>>该方法只接受一个参数：旋转的角度`angle`，它是固定顺时针方向的，以弧度为单位的值。旋转的中心点始终是`canvas`的原点，如果改变它，我们需要用到`translate`方法

来个对比：

```js
<script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        canCon.fillRect(0, 0, 150, 150)
        canCon.rotate(Math.PI / 4)
        canCon.fillRect(300, 100, 150, 150)
    </script>
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200109193528719.png" alt="image-20200109193528719" style="zoom:50%;" />

> - 注意，该方法旋转的是整个坐标系。
> - 该代码之后的所有坐标均按照新的坐标系来计算。
> - 犹如css的transform的旋转与平移，先旋转后平移 和 先平移后旋转时不一样的。

##### 2.3 缩放scale

> - 缩放用来增减图形在canvas中的像素数目，对形状，位图进行缩小或者放大
> - scale(x,y)>>>该方法可以缩放画布的水平和垂直的单位。两个参数都是实数，可以为负数。x为水平缩放因子，y为垂直缩放因子。如果比1小，会缩小图形，如果比1大会放大图形。默认为1，为实际大小。

> 没啥好演示的，直接上注意事项：
>
> 如果参数为负实数，相当于以x或y轴作为对称轴镜像反转

