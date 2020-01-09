### 1. canvas 文字绘制

> `canvas`提供了两种方法来渲染文本：
>
> - `fillText(text,x,y maxWidth?)`
> - 在指定的(x,y)位置填充指定的文本，绘制的最大宽度是可选的。如果最大宽度小于文字的实际大小的话，文字会被压缩，大于就没事。
>
> - `strokeText(text,x,y maxWidth?)`
> - 在指定的(x,y)位置绘制文本边框(空心文字)，绘制的最大宽度是可选的，`font = value`

> 文字的样式属性：`canCon.font = "48px serif"`

> 上代码：

```js
 <script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        canCon.font = "48px serif";
        canCon.fillText("hello world", 150, 150);
        canCon.strokeText("hello world", 150, 200);
    </script>
```

看效果：

<img src="C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200109134008553.png" alt="image-20200109134008553" style="zoom:50%;" />

> 文字绘制的其他属性：

| 属性               | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| textAlign = value  | 文本对齐选项。可选择包括start，end，left，right，center。默认为start |
| textBaseline=value | 基线对齐选项。可选项包括：top，hanging（文本基线是悬挂基线），middle，alphabetic（文字基线是标准的字母基线），ideographic（文字基线是表意字基线），如果字符本身超出了alphabetic基线，那么ideographic基线位置在字符本身的底部，buttom。默认是alphabetic |
| direction = value  | 文本方向。可选项包括：Itr,rtl,inherit。默认是inherit         |

> 再看看文字渲染的起始位置

```js
canCon.font = "50px serif";
canCon.fillText("hello world", 50, 50);
```

> 想要（50,50）成为文字的左上角
>
> 实际效果：

![](F:\Code\gitDemo\learn canvas\images\01.png)

> 实际情况是点（50,50）成为了文字的左下角开始位置

> 其实，这个起始坐标是基线的起始位置，并非文字的左上角

> 其他情况：
>
> 关于`textAlign` 这里面不建议去使用，因为文字的绘制可以通过坐标直接设置好，再用`textAlign` 会玩儿炸
>
> 关于基线，给个示意图自己细品：
>
> ![](F:\Code\gitDemo\learn canvas\images\基线示意图.jpg)
>
> 表意字和表音字：引用费尔迪南·德·索绪尔的观点，世界上的文字可总结为两种文字体系
>
> - 一个词用一个符号表示，这个符号与整个词发生关联，因此也就间接地和它所表达的观念产生关联，称之为表意文字，它不取决于符号发音。表意体系的典范是中国汉字。
> - 表音文字是以将语音中一连串连续的声音模写出来目的，有时是音节的，有时是字母的，即以言语中不能再缩减的要素为符号基础。表音体系的代表是英文。

### 2. canvas预测文本宽度

> 当你需要获得更多的文本细节时，下面的方法可以给你测量文本的方法

> 方法：`measureText()`
>
> 该方法返回一个`TextMetrics`对象的宽度、所在像素，这些体现文本特性的属性
>
> 话不多说是，上代码：

```js
<script>
        let canvas = document.querySelector("canvas"); //获取canvas元素
        let canCon = canvas.getContext("2d"); //获取canvas元素的渲染上下文
        canCon.font = "50px serif";
        var text = canCon.fillText("hello world", 50, 50);
        canCon.strokeText("hello world", 150, 200);
        console.log(canCon.measureText(text));
    </script>
```

> 看结果：

![image-20200109143547387](C:\Users\王雨波\AppData\Roaming\Typora\typora-user-images\image-20200109143547387.png)

