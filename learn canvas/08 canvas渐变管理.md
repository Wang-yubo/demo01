> 可以用线性或者径向的渐变来填充或者描边
>
> 用下面的方法新建一个`canvasGradient`对象，并且赋给图形的`fillStyle`或者`strokeStyle`属性

### 01. 线性渐变

> `createLinearGradient（x1,y1,x2,y2）`
>
> 该方法接受4个参数，表示渐变的起点（x1,y1）与终点（x2,y2）

> `name.addColorStop(position,"color")`
>
> 控制渐变的位置和渐变的颜色

> 来点例子：

```js
<script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        var lingrad = canCon.createLinearGradient(0, 0, 0, 150); //渐变色的尺寸数据
        lingrad.addColorStop(0, "yellow") //从上往下开始渐变，开始为蓝色
        lingrad.addColorStop(0.5, "skyblue"); //中间是天蓝色
        lingrad.addColorStop(0.5, "#fff") //立即切换为白色
        lingrad.addColorStop(1, "#bfc") //最后变为原谅绿

        var lingrad2 = canCon.createLinearGradient(0, 50, 0, 95);
        lingrad2.addColorStop(0.5, "black") //中间是黑色，省去了开始的位置
        lingrad2.addColorStop(1, "rgba(0,0,0,0)") //末尾透明
        canCon.fillStyle = lingrad;//填充渐变区域
        canCon.strokeStyle = lingrad2;//描边渐变
        canCon.fillRect(10, 10, 130, 130);//绘制的实心矩形的左上角坐标和宽高
        canCon.strokeRect(50, 50, 50, 50);//绘制的空心矩形的左上角坐标和宽高
    </script>
```

> 实际效果：

![image-20200108215655824](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108215655824.png)

### 02. 径向渐变

> `createRadialGradient(x1,y1,r1,x2,y2,r2)`
>
> 该方法接受6个参数，前三个定义一个以（x1,y1）为原点，半径为r1的圆，后三个定义另一个圆





### 03. 图案样式`patterns`

> 图案的应用跟渐变很类似的，创建出一个`pattern`之后，赋给`fillStyle`或者`strokeStyle`属性即可

> 方法：`createPatter(image,type)`
>
> 该方法接受两个参数：
>
> - image可以是一个`image`对象的引用，或者另一个`canvas`对象；
> - `type`（重复方式）必须是下面的字符串值之一：`repeat`，`repeat-x`，`repeat-y`和`no-repeat`

> 举个栗子：

```js
 <script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        var img = new Image();
        img.src = 'images/-2c18482ba29f7e54.jpg';
        img.onload = function() {
            var ptrn = canCon.createPattern(img, 'repeat');
            canCon.fillStyle = ptrn;
            canCon.fillRect(0, 0, 700, 700)
        }
    </script>
```

> 实际效果：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200108222740198.png" alt="image-20200108222740198" style="zoom:50%;" />

> 跟重复背景很相似

