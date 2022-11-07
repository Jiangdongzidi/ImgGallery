# 面试题

### 1、css盒模型

简介：就是用来装页面上的元素的矩形区域。CSS 中的盒子模型包括 IE 盒子模型和标 准的 W3C 盒子模型。 box-sizing(有 3 个值哦)：border-box,padding-box,content-box. 

标准盒子模型：

![image-20221102193723795](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221102193723795.png)

IE 盒子模型：

![image-20221102193750007](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221102193750007.png)

（1）**区别：**从图中我们可以看出，这两种盒子模型最主要的区别就是 width 的包含范围。 **在标准的盒子模型中，width 指 content 部分的宽度，在 IE 盒子模型中，width 表示 content+padding+border 这三个部分的宽度，**

（2）故这使得在计算整个盒子的宽度时存在 着**差异：** 标准盒子模型的盒子宽度：左右 border+左右 padding+width IE 盒子模型的盒子宽度：width 在 CSS3 中引入了 box-sizing 属性，box-sizing:content-box;表示标准的盒子模型， box-sizing:border-box 表示的是 IE 盒子模型 最后，前面我们还提到了，box-sizing:padding-box,这个属性值的宽度包含了左右 padding+width也很好理解性记忆，包含什么，width 就从什么开始算起。

#### 问题2：介绍一下盒模型

（1）CSS 盒模型本质上是一个盒子，封装周围的 HTML 元素，它包括：边距，边框，填充， 和实际内容。—— **padding + margin + border + content**

 （2）标准盒模型：一个块的总宽度=width+margin(左右)+padding(左右)+border(左右)

（3） 怪异盒模型：一个块的总宽度=width+margin（左右）（既 width 已经包含了 padding 和 border 值） 设置盒模型：box-sizing:border-box

#### 问题3：box-sizing

> box-sizing 规定两个并排的带边框的框。
>
> ​	语法为 box-sizing：content-box/borderbox/inherit

content-box：宽度和高度分别应用到元素的内容框，在宽度和高度之外绘制元素的内 边距和边框

border-box：为元素设定的宽度和高度决定了元素的边框盒。

inherit：继承父元素的 box-sizing

### 2、画一条0.5px的线

（1）采用 meta viewport 的方式 

```html
<meta name="viewport" content="initial-scale=1.0, maximum-scale=1.0, userscalable=no" />
<meta name="viewport" content="width=device-width,initial-sacle=0.5">
//width=device-width表示将viewport视窗的宽度调整为设备的宽度，这个宽度通常是指物理上宽度。
//缩放到原来的0.5倍，如果是1px那么就会变成0.5px
//viewport只针对于移动端，只在移动端上才能看到效果
```

（2）采用 border-image 的方式

（3）采用 transform: scale()的方式

```html
//画一条0.5px的线
<!DOCType html>
<html>
<head>
    <meta charset="utf-8">
    <style>
        .half-px {
            width: 300px;
            background-color: #000;
            height: 1px;
            transform: scale(0.5)
        }
    </style>
</head>
<body>
    <div class="half-px"></div>
</body>
</html>
```

### 3、transform属性

### 4、CSS3 图片边框 border-image

### 5、link 标签和 import 标签的区别 

（1）link 属于 html 标签，而@import 是 css 提供的 。

（2）页面被加载时，link 会同时被加载，而@import 引用的 css 会等到页面加载结束后加 载。 

（3）link 是 html 标签，因此没有兼容性，而@import 只有 IE5 以上才能识别。 link 方式样式的权重高于@import 的。

### 6、transition 和 animation 的区别 

（1）Animation 和 transition 大部分属性是相同的，他们都是随时间改变元素的属性值。 （2）他们的主要区别是：

​	① transition 需要触发一个事件才能改变属性，

​	② 而 animation 不需要 触发任何事件的情况下才会随时间改变属性值，并且 transition 为 2 帧，从 from .... to，而 animation 可以一帧一帧的。

### 7、flex布局

传统布局解决方案，基于盒状模型，依赖display属性+position属性+float属性。它对于哪些特殊布局非常不方便。比如垂直居中不容易实现。

##### （1）flex分为容器属性和元素属性

###### 1、容器属性：

​		fle-direction：决定主轴方向（即item的排列方法）

```css
.box {
flex-direction: row | row-reverse | column | column-reverse;
}
```

​		flex-wrap：决定换行规则

```css
.box{
flex-wrap: nowrap | wrap | wrap-reverse;
}
```

​		flex-flow：属性是 flex-direction 属性和 flex-wrap 属性的简写形式，默认值为 row nowrap；

```css
.box {
flex-flow: <flex-direction> || <flex-wrap>;
}
```

​		justify-content：对其方式，水平主轴对齐方式

​		align-items：对齐方式，竖直轴线方向

###### 2、项目属性（元素的属性）

​		order 属性：定义项目的排列顺序，顺序越小，排列越靠前，默认为 0。

​		flex-grow 属性：定义项目的**放大比例**，即使存在空间，也不会放大。

​		flex-shrink 属性：定义了项目的**缩小比例**，当空间不足的情况下会等比例的缩小，如 果定义个 item 的 flow-shrink 为 0，则为不缩小。

​		flex-basis 属性：定义了在分配多余的空间，项目占据的空间。

​		flex：是 flex-grow 和 flex-shrink、flex-basis 的简写，默认值为 0 1 auto。

​		align-self：允许单个项目与其他项目不一样的对齐方式，可以覆盖 align-items，默 认属性为 auto，表示继承父元素的 align-items。

### 8、BFC

用于清除浮动，仿制margin重叠等。

**块级格式化上下文，是一个独立的渲染区域，并且有一定的布局规则**。

（1）BFC不会与float box重叠

（2）BFC是页面上的一个独立容器，子元素不会影响外面

（3）计算BFC的高度时，浮动元素也会参与计算。

##### 1、开启BFC——根、浮、position、display、overflow

有根元 素，浮动元素，position 为 absolute 或 fixed 的元素，display 为 inline-block， table-cell，table-caption，flex，inline-flex，overflow 不为 visible 的元素

### 9、清除浮动

p44

#### 问题2：overflow 的原理 

（1）要讲清楚这个解决方案的原理，首先需要了解块格式化上下文，就是块格式化上下文是 CSS 可视化渲染的一部分，它是一块区域，规定了内部块盒 的渲染方式，以及浮动相互之间的影响关系。

 （2）当元素设置了 overflow 样式且值部位 visible 时，该元素就构建了一个 BFC，BFC 在 计算高度时，内部浮动元素的高度也要计算在内，也就是说技术 BFC 区域内只有一个 浮动元素，BFC 的高度也不会发生塌缩，所以达到了清除浮动的目的。

#### 问题3：清除浮动的方法 

给要清除浮动的元素添加样式 clear， 父元素结束标签钱插入清除浮动的块级元素，给该元素添加样式 clear 添加伪元素，在父级元素的最后，添加一个伪元素，通过清除伪元素的浮动，注意该 伪元素的 display 为 block， 父元素添加样式 overflow 清除浮动，overflow 设置除 visible 以外的任何位置

### 10、垂直居中方法

##### （1）margin： auto；

使用定位，子元素的top，left，right，bottom值设为0。margin设为auto。

**定位为上下左右为 0，margin：0 可以实现脱离文档流的居中.**

```html
 <style>
    div{
        width: 400px;
        height: 400px;
        position: relative;
        border: 1px solid #465468;
    }
    img{
        width: 50px;
        height: 50px;
        background-color: antiquewhite;
        position: absolute;
        margin: auto;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
    }
  </style>
</head>
<body>
    <div>
        <img src="mm.jpg">
    </div>       
</body>
```

![image-20221103194912906](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221103194912906.png)

##### (2)margin 负值法

**补充：其实这里也可以将 marin-top 和 margin-left 负值替换成， transform：translateX(-50%)和 transform：translateY(-50%)**

```html
<style>
    .container{
        width: 500px;
        height: 400px;
        border: 2px solid #379;
        position: relative;
    }
    .inner{
        width: 200px;
        height: 300px;
        background-color: #746;
        position: absolute;
        top: 50%;
        left: 50%;
        margin-top: -150px; /*height 的一半*/
        margin-left: -100px; /*width 的一半*/
    }

  </style>
</head>
<body>
    <div class="container">
        <img class="inner" src="mm.jpg">
    </div>       
</body>
```

![image-20221103200402591](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221103200402591.png)

##### （3）table-cell（未脱离文档流的）

**设置父元素的 display:table-cell,并且 vertical-align:middle，这样子元素可以实 现垂直居中。**

```html
 <style>
    div{
        width: 300px;
        height: 300px;
        border: 3px solid #555;
        display: table-cell;
        vertical-align: middle;
        text-align: center;
    }
    img{
        width: 150px;
        height: 150px;
        background-color: antiquewhite;
        vertical-align: middle;
    }

  </style>
</head>
<body>
    <div class="container">
        <img class="inner" src="mm.jpg">
    </div>       
</body>
```

![image-20221103200947153](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221103200947153.png)

##### （4）利用flex

**将父元素设置为 display:flex，并且设置 align-items:center;justifycontent:center;**

```html
 <style>
   .container{
        width: 300px;
        height: 200px;
        border: 3px solid #546461;
        display: -webkit-flex;
        display: flex;
        -webkit-align-items: center;
        align-items: center;
        -webkit-justify-content: center;
        justify-content: center;
    }
    .inner{
        border: 3px solid #458761;
        padding: 20px;
    }

  </style>
</head>
<body>
    <div class="container">
        <img class="inner" src="mm.jpg">
    </div>       
</body>
```

![image-20221103201406595](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221103201406595.png)

#### 问题2：如何实现图片在某个容器中居中

（1）margin：auto;

（2）margin 负值法

​	①父元素固定宽高，子元素设置 position: absolute，margin：  auto 平均分配 margin css3 属性 transform。                                     	②子元素设置 position: absolute; left: 50%; top: 50%;transform: translate(-50%,-50%);即可。  

（3）display：table

​	将父元素设置成 display: table, 子元素设置为单元格 display: table-cell。

（4）display：flex；

​	弹性布局 display: flex。设置 align-items: center; justify-content: center

#### 问题3：实现元素的垂直居中

法一：元素绝对定位，top:50%，margin-top：-（高度/2）

法二：高度不确定用 transform：translateY（-50%）

法三：父元素 display:flex,align-items:center;

法四：父元素 table 布局，子元素设置 vertical-align:center;

#### 问题4：有一个 width300，height300，怎么实现在屏幕上垂直水平居中

1、父级元素设置 text-alig：center，然后设置 line-height 和 vertical-align 使其 垂直居中，最后设置 font-size：0 消除近似居中的 bug 

2、父级元素设置 display：table-cell，vertical-align：middle 达到水平垂直居中 

3、采用绝对定位，原理是子绝父相，父元素设置 position：relative，子元素设置 position：absolute，然后通过 transform 或 margin 组合使用达到垂直居中效果，设 置 top：50%，left：50%，transform：translate（-50%，-50%）

 4、绝对居中，原理是当 top,bottom 为 0 时，margin-top&bottom 设置 auto 的话会无 限延伸沾满空间并平分，当 left，right 为 0 时,margin-left&right 设置 auto 会无限 延伸占满空间并平分，

 5、采用 flex，父元素设置 display：flex，子元素设置 margin：auto 6、视窗居中，vh 为视口单位，50vh 即是视口高度的 50/100，设置 margin：50vh auto 0，transform：translate(-50%)

### 11、关于 JS 动画和 css3 动画的差异性

（1）渲染线程分为mian thread 和 compositor thead 。

（2）如果css动画值改变transform和opacity，这时整个CSS动画得以在compositor thread 完成（而JS动画则会在main thread执行，然后触发compositor thread进行下一步操作）。

区别：功能涵盖面，JS比CSS大；	

实现/重构难度不一，CSS3比JS更加简单，性能跳优方向固定；

对帧速表现不好的低版本浏览器，css3可以做到自然降级；

css动画有天然事件支持，css3有兼容性问题。

#### 问题2：css动画如何实现

（1）**创建动画序列，需要使用 animation 属性或其子属性，**该属性允许配置动画时间、时 长以及其他动画细节。

（2）但该属性不能配置动画的实际表现，**动画的实际表现是 由 @keyframes 规则实现**，具体情况参见使用 keyframes 定义动画序列小节部分。

（3） transition 也可实现动画。**transition 强调过渡**，是元素的一个或多个属性发生变化 时产生的过渡效果，同一个元素通过两个不同的途径获取样式，而第二个途径当某种 改变发生（例如 hover）时才能获取样式，这样就会产生过渡动画。



