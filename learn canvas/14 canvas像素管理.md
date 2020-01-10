### 1. canvas 像素管理

##### 1.1 获取数据

> 为了获得一个包含画布场景像素数据的`ImageData`对象，可以用getImageData()方法：

```js
var myImageData = canCon.getImageData(left,top,width,height)
```

> 这个方法会返回一个`ImageData`对象，他代表了画布区域的对象数据，此画布的四个角落分别表示为`（left，top），（left+width，top），（left，top+height），以及（left+width，top+height）`四个点。这些坐标点被设定为画布坐标空间元素

> 你可以用`putImageData`()方法去对场景进行像素数据的写入
>
> dx和dy参数表示你希望在场景内左上角绘制的像素数据所得到的设备坐标

```js
canCon.putImageData(myImageData,dx,dy);
```

> 例如，为了在场景内左上角绘制`myImageData`代表的图片，你可以写

```js
canCon.putImageData(myImageData,0,0);
```

先来演示一番：

```js
 <script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        let img = new Image();
        let imageData;
        img.src = 'images/艺术 - 11.jpg';
        img.onload = function() {
            canCon.drawImage(img, 0, 0, 500, 500)
            imageData = canCon.getImageData(0, 0, 500, 500);
        }
    </script>
```

![image-20200110164743436](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110164743436.png)

![image-20200110165147083](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110165147083.png)

> 居然给我报了一个跨域问题的错

> 解决办法：用live server运行一下本地服务器
>
> ![image-20200110165742708](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110165742708.png)

> 现在可以调用imageData

![image-20200110165942658](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110165942658.png)

> 现在可以看到画布上的一切像素的信息了，

> 我们的图片是由500*500组成的，所以画布有25万个像素点，每个像素点有由4个数据组成，分别是r,g,b,a（red，green，blue，alpha），所以画布上有一百万个数据

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110170428866.png" alt="image-20200110170428866"  />

> 这里面又是4个数据为一组

![image-20200110170704055](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110170704055.png)

> 这四个数据从0~3分别是r，g，b，a。alpha255是由0~1转化为0~255的。想要0.8的透明度，直接255*0.8。

##### 1.2 写入数据

> 问：获得了上面的数据之后有什么用呢？
>
> 答：最简单的用法可以把这个数据画在别的位置

> 举个例子：利用刚刚所学知识，在另一个canvas画布里面复制一张图片

```html
<body>
    <canvas class="canvas1" width="500" height="500">如果浏览器版本过低，则此处文字会显示出来</canvas>
    <canvas class="canvas2" width="500" height="500">如果浏览器版本过低，则此处文字会显示出来</canvas>
    <script>
        let canvas1 = document.querySelector(".canvas1");
        let canCon1 = canvas1.getContext("2d");
        let canvas2 = document.querySelector(".canvas2");
        let canCon2 = canvas2.getContext("2d");

        let img = new Image();
        let imageData;
        img.src = 'images/艺术 - 11.jpg';
        img.onload = function() {
            canCon1.drawImage(img, 0, 0, 500, 500)
            imageData = canCon1.getImageData(0, 0, 500, 500);
            canCon2.putImageData(imageData, 0, 0)
        }
    </script>
</body>
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110173029504.png" alt="image-20200110173029504" style="zoom:50%;" />

> 获取了每一个像素的信息，当然是想怎么玩儿就怎么玩儿了啦

##### 1.3 数据格式

> - ImageData对象中存储着canvas对象真实的像素数据，它包含以下几个只读属性：
>   width：图片宽度，单位像素
> - height：图片高度，单位像素
> - data：包含着RGBA格式的整型数据，范围在0~255之间(包括255)

##### 1.4 创建数据

> 比如一张`500*500`大小的画布，25万个像素点，100万条数据，你完全可以通过自己定义每一个像素的信息，来组成一幅图片`500*500`的图片。头铁？硬核？

> 方法：创建一个新的，空白的ImageData对象，你应该会使用createImageData()。有两个2个版本的createImageData()方法：

```js
var myImageData = canCon.createImageData(width,height);
```

> 上面的代码创建了一个新的具体特定尺寸的ImageData对象。所有像素被预设为透明黑。
>
> 也可以创建一个被anotherImageData对象指定的相同像素的ImageData对象。这个新的对象像素全部被预设为透明黑。这个并非复制了图片数据。

```js
var myImageData = canCon.createImageData(anotherImageData);
```

> 头铁来了：设置一百万个数据

```js
 <script>
        let canvas1 = document.querySelector(".canvas1");
        let canCon1 = canvas1.getContext("2d");
        let canvas2 = document.querySelector(".canvas2");
        let canCon2 = canvas2.getContext("2d");

        let img = new Image();
        let imgData;
        img.src = 'images/艺术 - 11.jpg';
        let myImgData = canCon2.createImageData(500, 500);

        function random(min, max) {
            return Math.random() * (max - min) + min
        }

        for (let i = 0, len = myImgData.data.length; i < len; i++) {
            myImgData.data[i] = Math.floor(random(0, 255))
        }
        img.onload = function() {
            canCon1.drawImage(img, 0, 0, 500, 500)
            imgData = canCon1.getImageData(0, 0, 500, 500);
            canCon2.putImageData(myImgData, 0, 0)
        }
    </script>
```

![image-20200110180438281](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110180438281.png)

> ……你可真骚啊~