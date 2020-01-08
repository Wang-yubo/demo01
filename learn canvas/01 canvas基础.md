### 01. canvas的基本概念

> - canvas这个元素通常可以被用来在 HTML 页面中通过 JavaScript 进行绘制图形、合成图像等等操作，也可以用来做一些动画。
> - canvas由几组API构成，但并非所有浏览器都支持所有这些API。
> - 除了具备基本绘图能力的2D上下文，`canvas`还建议了一个名为WebGL的3D上下文。目前。支持该元素的浏览器都支持2D上下文及文本API，但是对WebGL（three.js就是利用WebGL）的支持还不够好
> - 要使用`canvas`元素，必须先设置其width和height属性，指定可绘图的区域大小。出现在开始和结束标签中的内容是后备信息，如果浏览不支持`canvas`元素，就会显示这些信息。（IE8及其以下版本）![image-20200107163105650](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107163105650.png)

### 02. canvas的默认样式

> ![image-20200107162647680](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107162647680.png)
>
> - 默认绘图区大小   width：300  ；height：150
> - 默认为行内元素 ，类似于img
> - 一般来说都要改成block，否则布局相当麻烦

### 03. canvas的尺寸概念

##### 3.1 css控制元素大小

> - css控制的元素大小并不是绘图区的大小
> - 设置了元素css，没设置width和height属性或是两者不一致，元素绘制时，图像会伸缩以适应css的尺寸；

![image-20200107165001200](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107165001200.png)

##### 3.2 width，height属性

> 这两个属性才是控制绘图区的大小

```html
<canvas width="500" height="500">如果浏览器版本过低，则此处文字会显示出来</canvas>
```

> 注意数字后面别加px...

### 04.  画图步骤

> 第一步：找到画布

```html
 <script>
        let canvas = document.querySelector("canvas")//获取canvas元素
        let canCon = canvas.getContext("2d")//获取canvas元素的渲染上下文
    </script>
```

> - `canvas`元素创造了一个可以自定义大小的画布，它公开了一个或多个渲染上下文，其可以用来绘制和处理要展示的内容
> - `canvas`元素有一个叫做`getContext（）`的方法，这个方法是用来获得渲染上下文和它的绘画功能。`getContext（）`只有一个参数，上下文格式，一般是2d，或者3d的WebGL

> 第二步：拿起笔，蘸上颜料

```js
canCon.fillStyle = "red";//canCon.fill拿起canvas画笔，style是画笔的颜色
```

> 第三步：构思画什么和怎么画：
>
> 画什么东西，用什么工具，画在什么位置等等

> 比如画个圆

```js
canCon.arc(250, 250, 66, 0, Math.PI * 2) //圆心的x,y,r,绘制方法
```

> 第四步：下笔作画

```js
canCon.fill(); //下笔作画
```

> 一个圆画好了

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107172831845.png" alt="image-20200107172831845" style="zoom:50%;" />

### 05. 画布栅格及坐标

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200107182124495.png" alt="image-20200107182124495" style="zoom:50%;" />

> - `canvas`中的原点在左上角
> - 网格中的一个单元相当于`canvas`元素中的一个像素
> - 显示器最小显示一个像素，所以不要写小数
> - 蓝色方块的左上角坐标为（x，y）

