### 1. canvas图像操作能力

> - `canvas`可以用于动态图像合成或者作为图形的背景，以及游戏界面（`sprites`）等等。
> - 浏览器支持的任意格式的外部图片都可以使用，比如，PNG、GIF、JPEG。甚至可以将同一个页面中其他`canvas`元素生成的图片作为图片源

##### 1.1 引入步骤

> 1. 获得一个指向`HTMLImageElement(即new Image())`的对象或者另一个`canvas`元素的引用作为源，也可以通过提供一个URL的方式来使用图片
> 2. 使用`drawImage()`函数将图片绘制到画布上
>
> `drawImage(image，x,y)`
>
> 其中`image`是`image`或者`canvas`对象，x和y是其在目标`canvas`里的起始坐标
>
> `drawImage(image，x,y，width，height)`
>
> 这个方法多了两个参数：`width`和`height`，这两个参数用来控制 当向canvas`画入时应该缩放的大小`

> 先简单地实现在canvas里加载一张图片

```js
 <script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文

        let img = new Image();
        img.src = "images/艺术 - 11.jpg"
        img.onload = function() {
            canCon.drawImage(img, 100, 192, 256, 144)
        }
```

![image-20200109150731676](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200109150731676.png)

##### 1.2 data：url base64

> - Base64就是一种基于64个可打印字符来表示二进制数据的方法。
> - 用记事本打开exe、jpg、pdf这些文件时，我们都会看到一大堆乱码，因为二进制文件包含很多无法显示和打印的字符，所以，如果要让记事本这样的文本处理软件能处理二进制数据，就需要一个二进制到字符串的转换方法。Base64是一种最常见的二进制编码方法。

> 优势是便于本地缓存，也可以随着网页加载直接发送过来，加快首屏加载速度
>
> 使用方法：可以将图片编码之后放在src里面，替换路径

##### 1.3 视频素材导入

> 视频素材的导入和图片导入一样的步骤
>
> 这里做个视频水印的例子：

```html
<body>
    <video src="video/QQ视频_0b6e35c5c4b24732f7d04cb1799eab1d1578497896.mp4" width="480" height="720"></video>
    <canvas width="480" height="720">如果浏览器版本过低，则此处文字会显示出来</canvas>
    <script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        let video = document.querySelector("video")
        video.addEventListener("play", function() {
            timerCallback();
        });
        var x = 100;

        function timerCallback() {
            if (video.paused || video.ended) {
                return
            }
            canCon.font = "200px";
            canCon.clearRect(0, 0, 480, 720);
            canCon.drawImage(video, 0, 0, 480, 720);
            canCon.fillText("这是一个特殊的水印", x += 0.01, 100)
            setInterval(function() {
                timerCallback()
            }, 1000 / 60)
        }
    </script>
</body>
```

![](F:\Code\gitDemo\learn canvas\images\导入视频.gif)

> 这里面`canCon.font`改变不了文字大小，目前还没找到原因

##### 1.5 图像切片

> `drawImage(image,sx,sy,sWidth,sHeight,dx,dy,dWidth,dHeight)`
>
> 第一个参数和其他的是相同的，都是一个图片或者一个`canvas`的引用。其他八个参数最好是参照下面的图解，前4个是定义图像源的切片位置和大小，后4个则是定义切片的目标显示位置和大小。

![](F:\Code\gitDemo\learn canvas\images\切片.jpg)

> 简单应用：

```js
 <script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        let img = new Image();
        img.src = 'images/-2c18482ba29f7e54.jpg'
        img.onload = function() {
            canCon.drawImage(img, 0, 0, 500, 500, 350, 350, 200, 200)
        }
    </script>
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200109184238467.png" alt="image-20200109184238467" style="zoom:50%;" />

