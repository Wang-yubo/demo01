### 01. 基本概念

> - 图形的基本元素是路径。
> - 路径是通过不同颜色和宽度的线段或者曲线相连接形成的不同形状的点的集合
> - 一个路径，甚至一个子路径都是闭合的

> 路径绘图的步骤：
>
> 1. 首先，创建路径起点
> 2. 然后使用画图命令去画出路径
> 3. 之后把路径封闭
> 4. 路径生成后，可以通过描边或者填充路径来渲染图形

| 命令        | 说明                                                       |
| ----------- | :--------------------------------------------------------- |
| beginPath() | 新建一条路径，生成之后，图形绘制命令被指定到路径上生成路径 |
| closePath() | 闭合路径之后图形绘制命令又重新指向上下文中                 |
| stroke()    | 通过实现来绘制图形轮廓                                     |
| fill()      | 通过填充路径的内容区生成实心的图形                         |
| moveTo()    | 将笔触移动到指定的坐标上                                   |
| lineTo()    | 绘制一条从当前位置到指定坐标的直线                         |

### 02. 绘制一个等腰三角形

```js
 <script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        canCon.beginPath();
        canCon.moveTo(250, 200);
        canCon.lineTo(300, 300);
        canCon.lineTo(200, 300);
        canCon.closePath();
        canCon.stroke()
    </script>
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107192428925.png" alt="image-20200107192428925" style="zoom:50%;" />

> 等边三角形会算出无理数，只能画出近似的等边三角形

### 03. 分段函数示例

```js
 <script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        canCon.beginPath();
        canCon.moveTo(20, 200);
        canCon.lineTo(20, 20);
        canCon.moveTo(20, 200);
        canCon.lineTo(200, 200);
        canCon.moveTo(75, 50);
        canCon.lineTo(100, 50);
        canCon.moveTo(100, 25);
        canCon.lineTo(125, 25);
        canCon.stroke()
    </script>
```

> 实际结果：



<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107193912287.png" alt="image-20200107193912287" style="zoom:50%;" />

> 图解：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107194003551.png" alt="image-20200107194003551" style="zoom:50%;" />

