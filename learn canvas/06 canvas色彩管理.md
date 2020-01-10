### 0.  `canvas`色彩管理

> 给图形上色有两个重要的属性可以做到
>
> - `fillStyle = "color"` 设置图形的填充显色
> - `strokeStyle = "color"` 设置图形轮廓的颜色
> - 默认情况下`fillStyle` 和`strokeStyle` 都是黑色

### 1. `fillStyle`

> 做个调色板：

```js
<script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        function createColorBoard(row, col) {
            for (var i = 0; i < row; i++) {
                for (var j = 0; j < col; j++) {
                    canCon.fillStyle = 'rgb(' + Math.floor(255 - (255 / row) * i) + ',' + Math.floor(255 - (255 / col) * j) + ',0)';
                    canCon.fillRect(j * 25, i * 25, 25, 25);
                }
            }
        }
        createColorBoard(10, 10)
    </script>
```

> 实际效果：

![image-20200108162159462](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108162159462.png)

### 2 strokeStyle

> 做个调色圈圈

```js
  <script>
        let canvas = document.querySelector("canvas") //获取canvas元素
        let canCon = canvas.getContext("2d") //获取canvas元素的渲染上下文
        function createColorBoard(row, col) {
            for (var i = 0; i < row; i++) {
                for (var j = 0; j < col; j++) {
                    canCon.strokeStyle = 'rgb(' + Math.floor(255 - (255 / row) * i) + ',' + Math.floor(255 - (255 / col) * j) + ',0)';
                    canCon.beginPath();
                    canCon.arc(12.5 + i * 25, 12.5 + j * 25, 10, 0, Math.PI * 2, true);
                    canCon.stroke();
                }
            }
        }
        createColorBoard(10, 10)
    </script>
```

实际效果：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108163037015.png" alt="image-20200108163037015" />

### 3 透明度(Transparency)

> - globalAlpha = transparencyValue
> - 这个属性影响canvas里所有图形的透明度
> - 有效范围0（完全透明）----1（完全不透明）
> - 默认为1
> - globalAlpha 属性在需要绘制大量拥有相同透明度的图形的时候相当高效

没设置全局透明时：

![image-20200108163037015](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108163037015.png)

> 设置全局透明后：

```js
  canCon.globalAlpha = 0.3;
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108164034907.png" alt="image-20200108164034907"  />

> **注意：在这行代码出现之前绘制的图形不会有透明效果，他只会影响该命令之后的代码。canvas是很注重代码顺序的。**

