### 1. canvas保存图片

> - 方法：`canvas.toDataURL('image/png,quality')`默认设定。创建一个PNG图片，格式是`bese64`格式
> - 你可以有选择的提供从0~1的品质质量，1表示最好，0基本不被辨析但有小的优势

> 在控制台操作：

```js
 canvas1.toDataURL('image/ycy.png')
```

> 返回结果：

![image-20200110203217628](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110203217628.png)

![image-20200110203247939](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110203247939.png)

> 根据编码，下载图片：

```html
<body>
    <canvas class="canvas1" width="500" height="500">如果浏览器版本过低，则此处文字会显示出来</canvas>
    <button>下载图片</button>
    <script>
        let canvas1 = document.querySelector(".canvas1");
        let canCon1 = canvas1.getContext("2d");
        let canvas2 = document.querySelector(".canvas2");
        let canCon2 = canvas2.getContext("2d");
        let btnDown = document.querySelector("button");
        let img = new Image();
        img.src = 'images/杨超越.jpg';
        img.onload = function() {
            canCon1.drawImage(img, 0, 0, 500, 500)
        }

        btnDown.onclick = function() {
            let base64 = canvas1.toDataURL('image/png', 1) //获取路径，此处可转码，换成其他格式即可
            let downA = document.createElement('a');
            downA.href = base64;
            downA.download = "杨超越.png"
            downA.click();
        }
    </script>
```

<img src="F:\Code\gitDemo\learn canvas\images\download.gif"  />

> 复习一下上传图片：

```html
 <input type="file">
```

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200110210615499.png" alt="image-20200110210615499" style="zoom:50%;" />

> 上传文件就是这么简单

