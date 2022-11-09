# 面试题

### 1、三栏布局的实现方式，尽可能多写，浮动布局时，三个 div 的生成顺序 有没有影响 

（1）flex布局

**设置三个 div 的父元素的 display: flex;然后设置中间 div 的 flex-grow: 1;（用于决定项目在有剩余空间的情况下是否放大，默认值为 0，即不放大）**

```html
<style type="text/css">
			.big {
				display: flex;
                width: 900;
			}
			.box1 {
				height: 300px;
				width: 100px;
				background-color: aquamarine;
			}
			.box2 {
				flex-grow: 1;
				background-color: cadetblue;
			} 
			.box3 {
				height: 300px;
				width: 100px;
				background-color: aqua;
			}
		</style>
	</head>
	<body>
		<div class="big">
			<div class="box1"></div>
			<div class="box2"></div>
			<div class="box3"></div>
		</div>
	</body>
```

![image-20221105160311763](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221105160311763.png)

2、float浮动

**设置左右两个 div 的 float 分别为 left 和 right，然后中间的 div 用 margin 撑开，用此方法时，三个 div 的生成顺序是：左、右、中。**

```html
<style type="text/css">
			.box1 {
				height: 300px;
				width: 100px;
				float: left;
				background-color: aquamarine;
			} 
			.box2 {
				height: 300px;
				margin: 0 105px 0 105px;
				background-color: cadetblue;
			} 
			.box3 {
				height: 300px;
				width: 100px;
				float: right;
				background-color: aqua;
			}
		</style>
	</head>
	<body>
			<div class="box1"></div>
			<div class="box3"></div>
			<div class="box2"></div>
	</body>
```

![image-20221105160417374](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221105160417374.png)

3、绝对定位 position: absolute

**左右两栏设置 position: absolute;设置右边 div 的偏移值，中间 div 用 margin 撑开。**

```html
<style type="text/css">
			*{
				margin: 0;
				padding: 0;
			}
			.box1 {
				height: 300px;
				width: 100px;
				position: absolute;
				background-color: aquamarine;
			}
 
			.box2 {
				height: 300px;
				margin: 0 105px 0 105px;
				background-color: cadetblue;
			}
 
			.box3 {
				height: 300px;
				width: 100px;
				position: absolute;
				top: 0;
				right: 0;
				background-color: aqua;
			}
		</style>
	</head>
	<body>
			<div class="box1"></div>
			<div class="box2"></div>
			<div class="box3"></div>
	</body>
```

![image-20221105160810030](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221105160810030.png)

#### 问题2：解决父元素display:flex布局下的子元素宽度无效问题

因为设置了display: flex; 导致block布局变成了flex布局， 所以在子元素宽度没有被撑破的情况下，子元素宽度是有效的，但是当子元素内容过多，此时宽度会比实际宽度小，所以如果想要在已经设置了flex布局的基础上，再进行子元素宽度的设置，可以应用下面的样式：（在该子元素上设置）

```css
width:120px;
flex-shrink: 0;
```

### 2、calc属性

Calc 用户动态计算长度值，任何长度值都可以使用 calc()函数计算，需要注意的是， 运算符前后都需要保留一个空格，例如：width: calc(100% - 10px)；

### 3、display：table 和本身的 table 有什么区别

（1）Display:table 和本身 table 是相对应的，

（2）**区别在于**，display：table 的 css 声明能 够让一个 html 元素和它的子节点像 table 元素一样，使用基于表格的 css 布局，是我 们能够轻松定义一个单元格的边界，背景等样式，而不会产生因为使用了 table 那样 的制表标签导致的语义化问题。

 （3）之所以现在逐渐淘汰了 table 系表格元素，是因为用 div+css 编写出来的文件比用 table 边写出来的文件小，而且 table 必须在页面完全加载后才显示，div 则是逐行显 示，table 的嵌套性太多，没有 div 简洁

### 4、如果想要改变一个 DOM 元素的字体颜色，不在它本身上进行操作？ 

答：可以更改父元素的color

### 5、用的最多的 css 属性是啥？ 

答：用的目前来说最多的是 flex 属性，灵活但是兼容性方面不强。

### 6、line-height 和 height 的区别 

（1）line-height 一般是指布局里面一段文字上下行之间的高度，是针对字体来设置的，

（2） height 一般是指容器的整体高度。

### 7、设置一个元素的背景颜色，背景颜色会填充哪些区域

答：background-color 设置的背景颜色会填充元素的 content、padding、border 区域。

### 8、inline-block、inline 和 block 的区别；为什么 img 是 inline 还可以 设置宽高 

##### （1）Block 块级元素

**其前后都会有换行符，能设置宽度，高度，margin/padding 水平 垂直方向都有效。**

1、block 元素会独占一行，多个 block 元素会各自新起一行。默认情况下，block 元素宽 度自动填满其父元素宽度。 

2、block 元素可以设置 width,height 属性。块级元素即使设置了宽度,仍然是独占一行。

3、 block 元素可以设置 margin 和 padding 属性。

##### （2） Inline

**设置 width 和 height 无效，margin 在竖直方向上无效，padding 在水平方向 垂直方向都有效，前后无换行符**

1、inline 元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不 下，才会新换一行，其宽度随元素的内容而变化。

2、inline 元素设置 width,height 属性无效。 

3、inline 元素的 margin 和 padding 属性，水平方向的 padding-left, padding-right, margin-left, margin-right 都产生边距效果；但竖直方向的 padding-top, paddingbottom, margin-top, margin-bottom 不会产生边距效果。 

##### （3）Inline-block

**能设置宽度高度，margin/padding 水平垂直方向 都有效，前后无换行 符**

inline-block：简单来说就是将对象呈现为 inline 对象，但是对象的内容作为 block 对象呈现。之后的内联对象会被排列在同一行内。

比如我们可以给一个 link（a 元 素）inline-block 属性值，使其既具有 block 的宽度高度特性又具有 inline 的同行特 性。

### 9、用 css 实现一个硬币旋转的效果

#### 问题2：CSS 画正方体，三角形 

### 10、了解重绘和重排吗，知道怎么去减少重绘和重排吗，让文档脱离文档流 有哪些方法 

##### 1、重排

​	DOM 的变化影响到了预算内宿的几何属性比如宽高，**浏览器重新计算元素的几何属性**， 其他元素的几何属性也会受到影响，**浏览器需要重新构造渲染书**，这个过程称之为重 排。

##### 2、重绘

浏览器将**受到影响的部分重新绘制在屏幕上** 的过程称为重绘。

##### 3、引起重排重绘的原因

 添加或者删除可见的 DOM 元素， 元素尺寸位置的改变 浏览器页面初始化， 浏览器窗口大小发生改变，**重排一定导致重绘，重绘不一定导致重排。** 

##### 4、减少重绘重排的方法有（动画，绝对定位脱离文档流）

 不在布局信息改变时做 DOM 查询， 使用 csstext,className 一次性改变属性 使用 fragment 对于多次重排的元素，比如说动画。使用绝对定位脱离文档流，使其不影响其他元素

#### 问题2：重排和重绘，讲讲看

1、**重绘**（repaint 或 redraw）：当盒子的位置、大小以及其他属性，例如颜色、字体大 小等都确定下来之后，浏览器便把这些原色都按照各自的特性绘制一遍，将内容呈现 在页面上。

重绘是指一个元素外观的改变所触发的浏览器行为，浏览器会根据元素的 新属性重新绘制，使元素呈现新的外观。 

**触发重绘的条件**：改变元素外观属性。如：color，background-color 等。 注意：table 及其内部元素可能需要多次计算才能确定好其在渲染树中节点的属性值， 比同等元素要多花两倍时间，这就是我们尽量避免使用 table 布局页面的原因之一。 

2、**重排**（重构/回流/reflow）：当渲染树中的一部分(或全部)因为元素的规模尺寸，布 局，隐藏等改变而需要重新构建, 这就称为回流(reflow)。每个页面至少需要一次回 流，就是在页面第一次加载的时候

3、**重绘和重排的关系**：在回流的时候，浏览器会使渲染树中受到影响的部分失效，并重 新构造这部分渲染树，完成回流后，浏览器会重新绘制受影响的部分到屏幕中，该过 程称为重绘。所以，重排必定会引发重绘，但重绘不一定会引发重排。

