# 面试题

### 1、说一下块元素和行元素

块元素：独占一行，并且有自动填满父元素，可以设置margin和padding以及高度和宽度。

行元素：不会独占一行，width和height会失效，并且在垂直方向的padding和margin会失效。

### 2、多行元素文本省略（文本溢出处理）

```html
 <style>
    .txt-cut {
            width: 200px;
            background-color: antiquewhite;
			overflow: hidden;
			text-overflow: ellipsis;  //  文本以省略号显示 
			display: -webkit-box;  // 将盒子转换为弹性盒子
			-webkit-line-clamp: 3;  //  设置显示多少行
			-webkit-box-orient: vertical;  // 文本显示方式，默认水平
		}

  </style>
</head>
<body>
    <div class="container">
       <div class="txt-cut">这是一行多行文本溢出的文字这是一行多行文本溢出的文字
            这是一行多行文本溢出的文字这是一行多行文本溢出的文字
            这是一行多行文本溢出的文字这是一行多行文本溢出的文字
            这是一行多行文本溢出的文字这是一行多行文本溢出的文字
            这是一行多行文本溢出的文字这是一行多行文本溢出的文字
            </div>
    </div>       
```

![image-20221105140417131](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221105140417131.png)

##### 单行元素的文本省略号

```html
<style>
    .single-cut {
        width: 100px;
        background-color: antiquewhite;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
    }

  </style>
</head>
<body>
    <div class="container">
        <div class="single-cut">单行文本省略号单行文本省略号单行文本省略号单行文本省略号单行文本省略号
        </div>
    </div>       
</body>
```

![image-20221105140856360](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221105140856360.png)

#### 问题2：css3中对溢出的处理

text-overflow 属性，值为 clip 是修剪文本；ellipsis 为显示省略符号来表被修剪的 文本；string 为使用给定的字符串来代表被修剪的文本。

### 3、visibility=hidden, opacity=0，display:none区别

#####  1、visibility=hidden

**visibility显示或隐藏元素而不改变文档的布局。不会触发元素已绑定事件**

（1）DOM 结构：元素被隐藏，但是会被渲染不会消失，占据空间；
（2）事件监听：无法进行 DOM 事件监听；
（3）性 能：动态改变此属性时会引起重绘，性能较高；
（4）继 承：会被子元素继承，子元素可以通过设置 visibility: visible; 来取消隐藏；
（5）transition：不支持 display。

##### 2、opacity=0

**opacity=0；该元素隐藏起来了，但不会改变页面布局，会触发已绑定事件**。

（1）DOM 结构：透明度为 100%，元素隐藏，占据空间；
（2）事件监听：可以进行 DOM 事件监听；
（3）性 能：提升为合成层，不会触发重绘，性能较高；
（4）继 承：会被子元素继承,且，子元素并不能通过 opacity: 1 来取消隐藏；
（5）transition：不支持 opacity。

##### 3、display:none; 

**display:none；把元素隐藏起来，会改变页面布局，可以理解成在页面中把元素删除掉一样。**

1. DOM 结构：浏览器不会渲染 `display` 属性为 `none` 的元素，不占据空间；
2. 事件监听：无法进行 DOM 事件监听；
3. 性能：动态改变此属性时会引起重排，性能较差；
4. 继承：不会被子元素继承，毕竟子类也不会被渲染；
5. transition： 不支持 `display`。

#### 问题2：怎么样让一个元素消失

答：visibility=hidden, opacity=0，display:none

#### 问题3：隐藏某个元素的方法

答：display:none; visibility:hidden; opacity: 0; position 移到外部，z-index 涂层 遮盖等等

### 4、双边距重叠问题

多个相邻（兄弟伙父子关系）普通流的**块元素垂直方向margin会重叠**

两个相邻外边距折叠结果：

| 两个相邻的外边距 | 折叠结果               |
| ---------------- | ---------------------- |
| 都是正数（++）   | 两者之间较大的值       |
| 都是负数（- - ） | 两者之间较绝对值大的值 |
| 一正一负（+ -）  | 是两者的相加的和       |

### 5、position属性  比较

##### 1、固定定位  fixed

元素的位置相对于浏览器窗口是固定位置，即使窗口是滚动的它也不会移动。

**Fixed 定 位使元素的位置与文档流无关，因此不占据空间。 Fixed 定位的元素和其他元素重 叠。**

##### 2、相对定位relative

如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置**垂 直或水平位置**，让这个元素“相对于”它的起点进行移动。

 在使用相对定位时，无论 是否进行移动，元素仍然占据原来的空间。因此，移动元素会导致它覆盖其它框。

##### 3、绝对定位absolute

绝对定位的元素的位置相对于最近的**已定位父元素**，如果元素没有已定位的父元素， 那么它的位置相对于<html>。 

**absolute 定位使元素的位置与文档流无关，因此不占 据空间**。 absolute 定位的元素和其他元素重叠。

##### 4、粘性定位sticky

元素先按照普通文档流定位，然后相对于该元素在流中的 flow root（BFC）和 containing block（最近的块级祖先元素）定位。而后，元素定位表现为在跨越特定 阈值前为相对定位，之后为固定定位。

##### 5、默认定位static

默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。

##### 6、inherit

规定应该从父元素继承 position 属性的值。

#### 问题2：position 属性的值有哪些及其区别

Position 属性把元素放置在一个静态的，相对的，绝对的，固定的位置中，

（1） Static：位置设置为 static 的元素，他始终处于页面流给予的位置，static 元素会忽 略任何 top,buttom,left,right 声明 

（2）Relative：位置设置为 relative 的元素，可将其移至相对于其正常位置的地方，因此 left：20 会将元素移至元素正常位置左边 20 个像素的位置

（3） Absolute：此元素可定位于相对包含他的元素的指定坐标，此元素可通过 left，top 等属性规定 （4）Fixed：位置被设为 fiexd 的元素，可定为与相对浏览器窗口的指定坐标，可以通过 left，top，right 属性来定位

### 7、z-index的定位方法



### 8、css3新特性

（1）在布局方面新增了 flex 布局，

（2）在选择器方面新增了例如 first-oftype,nth-child 等选择器，

（3）在盒模型方面添加了 box-sizing 来改变盒模型，

（4）在动画方 面增加了 animation，2d 变换，3d 变换等，

（5）在颜色方面添加透明，rbga 等，

（6）在字体方 面允许嵌入字体和设置字体阴影，最后还有媒体查讯等

### 9、css选择器优先级

答：（1）id 选择器，class 选择器，标签选择器，伪元素选择器，伪类选择器等 同一元素引用了多个样式时，排在后面的样式属性的优先级高； 

（2）样式选择器的类型不同时，优先级顺序为：id 选择器 > class 选择器 > 标签选择 器； 标签之间存在层级包含关系时，后代元素会继承祖先元素的样式。如果后代元素定义 了与祖先元素相同的样式，则祖先元素的相同的样式属性会被覆盖。继承的样式的优 先级比较低，至少比标签选择器的优先级低； 

（3）带有!important 标记的样式属性的优先级最高；

（4） 样式表的来源不同时，优先级顺序为：内联样式> 内部样式 > 外部样式 > 浏览器用 户自定义样式 > 浏览器默认样式

#### 问题2：知道属性选择器和伪类选择器的优先级吗 

答：属性选择器和伪类选择器优先级相同

问题3：css 的常用选择器 

答：id 选择器，类选择器，伪类选择器等

### 10、float的元素，display是什么

答：display 为 block







