### 01. 管理阴影基本参数

| 属性                  | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| shadowOffsetX = value | 用来设定阴影在X轴的延伸距离，不受变换矩阵所影响，负值表示向左移动，正值向右，默认为0 |
| shadowOffsetY = value | 用来设定阴影在Y轴的延伸距离，不受变换矩阵所影响，负值表示向上移动，正值向下，默认为0 |
| shadowBlur = value    | 用于设定阴影的模糊程度，其数值并不跟像素挂钩，也不受变换矩阵的影响，默认为0 |
| shadowColor = color   | 是标准的颜色值，用于设定阴影颜色效果，默认是全透明的黑色     |

先上代码：

```js
<script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文

        canCon.shadowOffsetX = 200;
        canCon.shadowOffsetY = 200;
        canCon.shadowBlur = 20;
        canCon.shadowColor = "red";
        var img = new Image();
        img.src = 'images/-2c18482ba29f7e54.jpg';
        img.onload = function() {
            var ptrn = canCon.createPattern(img, 'no-repeat');
            canCon.fillStyle = ptrn;
            canCon.fillRect(0, 0, 700, 700)
        }
    </script>
```

> - 这四个属性都是类似全局的
> - 不用加px

> 实际效果：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108230044774.png" alt="image-20200108230044774" style="zoom:50%;" />

### 02. 线性管理填充规则

> 当我们用到fill时，你可以选择一个填充规则，该规则根据某处在路径路径的外面或者里面来决定是否被填充，这对于自己与自己路径相交或者路径被嵌套的时候是有用的

> 两个可能的值：
>
> - `nonzero` 全部填充，默认值
> - `evennodd` 奇偶数区域填充

> 老板，来两个栗子：

```js
<script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文

        canCon.beginPath();
        canCon.arc(50, 50, 30, 0, Math.PI * 2, true);
        canCon.arc(50, 50, 15, 0, Math.PI * 2, true);
        canCon.arc(50, 50, 45, 0, Math.PI * 2, true);
        canCon.fill("nonzero")
    </script>
```

`nonzero`全部填充时：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108231526215.png" alt="image-20200108231526215"  />

>  奇填偶不填，符号看……看个鬼

```js
 canCon.fill("evenodd")
```

> 现在的效果：

![image-20200108231802487](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108231802487.png)

> 但是这奇偶很诡异，有些实际情况没有奇偶的分别就全部渲染，能分别奇偶就分别渲染

### 03. Path2D对象

> - 正如我们在前面例子中看到的，你可以使用一些列的路径和绘画命令来吧对象“画”在画布上。
> - 为了简化代码和提高性能，Path2D对象已经可以在较新版本的浏览器中使用，用来缓存或者记录绘画命令，这样你将快速地回顾路径。

> Path2D()会返回一个新初始化的Path2D对象
>
> ```js
> new Path2D();//空的Path2D对象
> new Path2D(path)；克隆Path对象
> ```

> 小哥哥，来一包栗子：

```js
 <script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文

        var path1 = new Path2D();
        path1.rect(10, 10, 100, 100);
        var path2 = new Path2D(path1);
        path2.moveTo(220, 60);
        path2.arc(170, 60, 50, 0, Math.PI * 2);
        canCon.stroke(path2)
    </script>
```

> 孩子给，你要的栗子：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108233433110.png" alt="image-20200108233433110" style="zoom:100%;" />

