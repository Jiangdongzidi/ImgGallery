#  面试题

### 1、get 请求传参长度的误区 

> **误区**：我们经常说 get 请求参数的大小存在限制，而 post 请求的参数大小是无限制 的。

 实际上 HTTP 协议从未规定 GET/POST 的请求长度限制是多少。对 get 请求参数的限制 是来源与浏览器或 web 服务器，浏览器或 web 服务器限制了 url 的长度。

为了明确这 个概念，我们必须**再次强调下面几点**: **HTTP 协议 未规定 GET 和 POST 的长度限制 GET 的最大长度显示。是因为 浏览器和 web 服务器限制了 URI 的长度。 不同的浏览器和 WEB 服务器，限制的最大长度不一样 。**

要支持 IE，则最大长度为 `2083byte`，若只支持 Chrome，则最大长度 `8182byte`

### 2、补充 get 和 post 请求在缓存方面的区别 

（1）get 请求类似于查找的过程，用户获取数据，可以不用每次都与数据库连接，所以可以 使用缓存。 

（2）post 不同，post 做的一般是修改和删除的工作，所以必须与数据库交互，所以不能使 用缓存。因此 get 请求适合于请求缓存。

### 3、说一下闭包

闭包就是能够**读取其他函数内部变量的函数**，或者子函数在外调用，子函数所在的父函数的作用域不会被释放。

### 4、说一下类的创建和继承 

（1）类的创建（es5）：new 一个 function，在这个 function 的 prototype 里面增加 属性和方法。

下面来创建一个 Animal 类：

```javascript
// 定义一个动物类
function Animal (name) {
	// 属性
	this.name = name || 'Animal';
	// 实例方法
    this.sleep = function(){
        console.log(this.name + '正在睡觉！');
    }
}
// 原型方法
Animal.prototype.eat = function(food) {
	console.log(this.name + '正在吃：' + food);
};
```

这样就生成了一个 Animal 类，实力化生成对象后，有方法和属性。

（2）类的继承——原型链继承

```javascript
function Cat(){ }
    Cat.prototype = new Animal();
    Cat.prototype.name = 'cat';
// Test Code
    var cat = new Cat();
    console.log(cat.name);
    console.log(cat.eat('fish'));
    console.log(cat.sleep());
    console.log(cat instanceof Animal); //true
    console.log(cat instanceof Cat); //true
```

介绍：在这里我们可以看到 new 了一个空对象,这个空对象指向 Animal 并且 Cat.prototype 指向了这个空对象，这种就是基于原型链的继承。 

特点：基于原型链，既是父类的实例，也是子类的实例

 缺点：无法实现多继承

（3）构造继承：使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给 子类（没用到原型）

```javascript
function Cat(name){
    Animal.call(this);
    this.name = name || 'Tom';
}
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // false
console.log(cat instanceof Cat); // true
```

特点：可以实现多继承 

缺点：只能继承父类实例的属性和方法，不能继承原型上的属性和方法

（4）实例继承和拷贝继承 实例继承：为父类实例添加新特性，作为子类实例返回 拷贝继承：拷贝父类元素上的属性和方法 上述两个实用性不强，不一一举例。 

（5）组合继承：相当于构造继承和原型链继承的组合体。通过调用父类构造，继承父 类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

```javascript
function Cat(name){
    Animal.call(this);
    this.name = name || 'Tom';
}
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); // true
```

特点：可以继承实例属性/方法，也可以继承原型属性/方法 

缺点：调用了两次父类构造函数，生成了两份实例

（6）寄生组合继承：通过寄生方式，砍掉父类的实例属性，这样，在调用两次父类的 构造的时候，就不会初始化两次实例方法/属性

```javascript
function Cat(name){
    Animal.call(this);
    this.name = name || 'Tom';
}
(function(){
	// 创建一个没有实例方法的类
    var Super = function(){};
    Super.prototype = Animal.prototype;
    //将实例作为子类的原型
    Cat.prototype = new Super();
})();
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); //true
```



### 5、如何解决异步回调地狱 

答：promise、generator、async/await

### 6、说说前端中的事件流 

HTML 中与 javascript 交互是通过事件驱动来实现的，例如鼠标点击事件 onclick、页 面的滚动事件 onscroll 等等，可以向文档或者文档中的元素添加事件侦听器来预订事 件。想要知道这些事件是在什么时候进行调用的，就需要了解一下“事件流”的概 念。

#####  1、什么是事件流：

事件流描述的是从页面中接收事件的顺序,DOM2 级事件流包括下面几个 阶段。 

> 事件捕获阶段 
>
> 处于目标阶段 
>
> 事件冒泡阶段

addEventListener：addEventListener 是 DOM2 级事件新增的指定事件处理程序的操 作，这个方法接收 3 个参数：要处理的事件名、作为事件处理程序的函数和一个布尔 值。最后这个布尔值参数如果是 true，表示在**捕获阶段**调用事件处理程序；如果是 false，表示在**冒泡阶段**调用事件处理程序。 

**IE 只支持事件冒泡。**

### 7、如何让事件先冒泡后捕获

 答：在 DOM 标准事件模型中，是先捕获后冒泡。但是如果要实现先冒泡后捕获的效果，**对 于同一个事件，监听捕获和冒泡，分别对应相应的处理函数，监听到捕获事件，先暂缓执行，直到冒泡事件被捕获后再执行捕获之间。**

### 8、说一下事件委托 （ul和li）

简介：事件委托指的是，不在事件的发生地（直接 dom）上设置监听函数，而是在其父 元素上设置监听函数，通过事件冒泡，父元素可以监听到子元素上事件的触发，通过 判断事件发生元素 DOM 的类型，来做出不同的响应。

 举例：最经典的就是 ul 和 li 标签的事件监听，比如我们在添加事件时候，采用事件 委托机制，不会在 li 标签上直接添加，而是在 ul 父元素上添加。 

好处：比较合适动态元素的绑定，新添加的子元素也会有监听函数，也可以有事件触 发机制。

### 9、说一下图片的懒加载和预加载 

##### 1、预加载和懒加载

**预加载**：**提前加载图片，**当用户需要查看时可直接从**本地缓存中渲染**。

**懒加载**：懒加载的主要目的是作为服务器前端的优化，减少请求数或延迟请求数。

两种技术的本质：两者的行为是相反的，一个是提前加载，一个是迟缓甚至不加载。 **懒加载对服务器前端有一定的缓解压力作用**，预加载则会增加服务器前端压力。

#### 问题2：什么是按需加载 

答：当用户触发了动作时才加载对应的功能。触发的动作，是要看具体的业务场景而言， 包括但不限于以下几个情况：鼠标点击、输入文字、拉动滚动条，鼠标移动、窗口大 小更改等。加载的文件，可以是 JS、图片、CSS、HTML 等。

### 10、mouseover 和 mouseenter 的区别

1、mouseover：当鼠标移入元素或其子元素都会触发事件，所以有一个重复触发，冒泡的 过程。对应的移除事件是 mouseout

2、mouseenter：当鼠标移除元素本身（不包含元素的子元素）会触发事件，也就是不会 冒泡，对应的移除事件是 mouseleave

### 11、JS 的 new 操作符做了哪些事情

答：new 操作符新建了一个空对象，这个对象原型指向构造函数的 prototype，执行构造函 数后返回这个对象。

### 12、改变函数内部 this 指针的指向函数（bind，apply，call 的区别） 

答：（1）通过 apply 和 call 改变函数的 this 指向。

第一个参数都是一样的表 示要改变指向的那个对象。

第二个参数，apply 是数组，而 call 则是 arg1,arg2...这 种形式。

（2）通过 bind 改变 this 作用域会返回一个新的函数，这个函数不会马上执行。

### 13、JS 的各种位置，clientHeight,scrollHeight,offsetHeight ,以 及 scrollTop, offsetTop,clientTop 的区别？ 

（1）clientHeight：表示的是可视区域的高度，不包含 border 和滚动条 

（2）offsetHeight：表示可视区域的高度，包含了 border 和滚动条 

（3）scrollHeight：表示了所有区域的高度，包含了因为滚动被隐藏的部分。 

（4）clientTop：表示边框 border 的厚度，在未指定的情况下一般为 0 

（5）scrollTop：滚动后被隐藏的高度，获取对象相对于由 offsetParent 属性指定的父坐 标(css 定位的元素或 body 元素)距离顶端的高度。

### 14、JS 拖拽功能的实现 

首先是三个事件，分别是 mousedown，mousemove，mouseup 当鼠标点击按下的时候，需要一个 tag 标识此时已经按下，可以执行 mousemove 里面 的具体方法。

1、clientX，clientY 标识的是鼠标的坐标，分别标识横坐标和纵坐标，

2、并且我们用 offsetX 和 offsetY 来表示元素的元素的初始坐标，移动的举例应该是： 鼠标移动时候的坐标-鼠标按下去时候的坐标。 

3、也就是说定位信息为： `鼠标移动时候的坐标-鼠标按下去时候的坐标+元素初始情况下的 offetLeft.` 4、还有一点也是原理性的东西，也就是拖拽的同时是绝对定位，我们改变的是绝对定位 条件下的 left 以及 top 等等值。 

补充：也可以通过 html5 的拖放（Drag 和 drop）来实现

### 15、异步加载 JS 的方法

1、defer：只支持 IE 如果您的脚本不会改变文档的内容，可将 defer 属性加入到<script>标签中，以便加快处理文档的速度。因为浏览器知道它将能够安全地读取文档的剩余部分而不用执行脚本，它将推迟对脚本的解释，直到文档已经显示给用户为 止。 

2、async，HTML5 属性仅适用于外部脚本，并且如果在 IE 中，同时存在 defer 和 async， 那么 defer 的优先级比较高，脚本将在页面完成时执行。 创建 script 标签，插入到 DOM 中。

### 16、Ajax 解决浏览器缓存问题 

1、在 ajax 发送请求前加上 anyAjaxObj.setRequestHeader("If-ModifiedSince","0")。

2、在 ajax 发送请求前加上 anyAjaxObj.setRequestHeader("Cache-Control","nocache")。

3、在 URL 后面加上一个随机数： "fresh=" + Math.random()。

4、在 URL 后面加上时间搓："nowtime=" + new Date().getTime()。

5、如果是使用 jQuery，直接这样就可以了 $.ajaxSetup({cache:false})。这样页面的所 有 ajax 都会执行这条语句就是不需要保存缓存记录。

### 17、JS的节流和防抖

### 18、JS中的垃圾回收机制

​	必要性：由于字符串、对象和数组没有固定大小，所有当他们的大小已知时，才能对 他们进行动态的存储分配。JavaScript 程序每次创建字符串、数组或对象时，解释器 都必须分配内存来存储那个实体。只要像这样动态地分配了内存，最终都要释放这些 内存以便他们能够被再用，否则，JavaScript 的解释器将会消耗完系统中所有可用的 内存，造成系统崩溃。

​	这段话解释了为什么需要系统需要垃圾回收，JS 不像 C/C++，他有自己的一套垃圾回 收机制（Garbage Collection）。JavaScript 的解释器可以检测到何时程序不再使用 一个对象了，当他确定了一个对象是无用的时候，他就知道不再需要这个对象，可以 把它所占用的内存释放掉了。例如：

```javascript
var a="hello world";
var b="world";
var a=b;
//这时，会释放掉"hello world"，释放内存以便再引用
```

#### 垃圾回收的方法：标记清除、计数引用。

##### 1、标记清除

​	这是最常见的垃圾回收方式，当变量进入环境时，就标记这个变量为”进入环境“,从 逻辑上讲，永远不能释放进入环境的变量所占的内存，永远不能释放进入环境变量所 占用的内存，只要执行流程进入相应的环境，就可能用到他们。当离开环境时，就标 记为离开环境。 垃圾回收器在运行的时候会给存储在内存中的变量都加上标记（所有都加），然后去 掉环境变量中的变量，以及被环境变量中的变量所引用的变量（条件性去除标记）， 删除所有被标记的变量，删除的变量无法在环境变量中被访问所以会被删除，最后垃 圾回收器，完成了内存的清除工作，并回收他们所占用的内存。 

##### 2、引用计数法

 另一种不太常见的方法就是引用计数法，引用计数法的意思就是每个值没引用的次 数，当声明了一个变量，并用一个引用类型的值赋值给改变量，则这个值的引用次数 为 1,；相反的，如果包含了对这个值引用的变量又取得了另外一个值，则原先的引用 值引用次数就减 1，当这个值的引用次数为 0 的时候，说明没有办法再访问这个值了， 因此就把所占的内存给回收进来，这样垃圾收集器再次运行的时候，就会释放引用次 数为 0 的这些值。 

用引用计数法会存在内存泄露，下面来看原因：

```javascript
function problem() {
var objA = new Object();
var objB = new Object();
objA.someOtherObject = objB;
objB.anotherObject = objA;
}
```

​	在这个例子里面，objA 和 objB 通过各自的属性相互引用，这样的话，两个对象的引用 次数都为 2，在采用引用计数的策略中，由于函数执行之后，这两个对象都离开了作用 域，函数执行完成之后，因为计数不为 0，这样的相互引用如果大量存在就会导致内存 泄露。

特别是在 DOM 对象中，也容易存在这种问题：

```javascript
var element=document.getElementById（’‘）；
var myObj=new Object();
myObj.element=element;
element.someObject=myObj;
```

这样就不会有垃圾回收的过程。

### 19、eval 是做什么的 

答：它的功能是将对应的字符串解析成 JS 并执行，应该避免使用 JS，因为非常消耗性能 （2 次，一次解析成 JS，一次执行）

### 20、如何理解前端模块化

前端模块化就是复杂的文件编程一个一个独立的模块，比如 JS 文件等等，分成独立的 模块有利于重用（复用性）和维护（版本迭代），这样会引来模块之间相互依赖的问 题，所以有了 commonJS 规范，AMD，CMD 规范等等，以及用于 JS 打包（编译等处理） 的工具 webpack。

### 21、说一下 CommonJS、AMD 和 CMD 

一个模块是能实现特定功能的文件，有了模块就可以方便的使用别人的代码，想要什 么功能就能加载什么模块。

##### 1、CommonJS

开始于服务器端的模块化，同步定义的模块化，每个模块都是一个单独的 作用域，模块输出，modules.exports，模块加载 require()引入模块。

#####  2、AMD

中文名异步模块定义的意思。 requireJS 实现了 AMD 规范，主要用于解决下述两个问题。

（1）多个文件有依赖关系，被依赖的文件需要早于依赖它的文件加载到浏览器 

（2）加载的时候浏览器会停止页面渲染，加载文件越多，页面失去响应的时间越长。 语法：requireJS 定义了一个函数 define，它是全局变量，用来定义模块。 

requireJS 的例子：

```javascript
//定义模块
define(['dependency'], function(){
var name = 'Byron';
function printName(){
console.log(name);
}
return {
printName: printName
};
});
//加载模块
require(['myModule'], function (my){
my.printName();
}
RequireJS 定义了一个函数 define,它是全局变量，用来定义模块：
define(id?dependencies?,factory)
```

在页面上使用模块加载函数： require([dependencies],factory)； 

总结 AMD 规范：require（）函数在加载依赖函数的时候是异步加载的，这样浏览器不 会失去响应，它指定的回调函数，只有前面的模块加载成功，才会去执行。 因为网页在加载 JS 的时候会停止渲染，因此我们可以通过异步的方式去加载 JS,而如 果需要依赖某些，也是异步去依赖，依赖后再执行某些方法。