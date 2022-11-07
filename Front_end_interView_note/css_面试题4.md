# 面试题

### 1、两个嵌套的 div，position 都是 absolute，子 div 设置 top 属性，那么 这个 top 是相对于父元素的哪个位置定位的。

答：margin 的外边缘

### 2、display取值

> [display取值]: https://developer.mozilla.org/zh-CN/docs/Web/CSS/display

答:主要取值有 none,block,inline-block,inline,flex 等

3、css布局

六种布局方式总结：圣杯布局、双飞翼布局、Flex 布局、绝对定位布局、表格布局、 网格布局。

##### 1、圣杯布局

是指布局从上到下分为 header、container、footer，然后 container 部分定 为三栏布局。这种布局方式同样分为 header、container、footer。

圣杯布局的缺陷在 于 center 是在 container 的 padding 中的，因此宽度小的时候会出现混乱。 

##### 2、双飞翼布局

给 center 部分包裹了一个 main 通过设置 margin 主动地把页面撑开。 

##### 3、Flex 布局

是由 CSS3 提供的一种方便的布局方式。 

##### 4、绝对定位布局

是给 container 设置 position: relative 和 overflow: hidden，因为 绝对定位的元素的参照物为第一个 postion 不为 static 的祖先元素。 left 向左浮 动，right 向右浮动。center 使用绝对定位，通过设置 left 和 right 并把两边撑 开。 center 设置 top: 0 和 bottom: 0 使其高度撑开。 

##### 5、表格布局

好处是能使三栏的高度统一。 

##### 6、网格布局

可能是最强大的布局方式了，使用起来极其方便，但目前而言，兼容性并不 好。网格布局，可以将页面分割成多个区域，或者用来定义内部元素的大小，位置， 图层关系。

### 3、css 预处理器有什么 

答：less，sass 等
