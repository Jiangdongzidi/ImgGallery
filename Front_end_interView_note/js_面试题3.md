# 面试题

### 1、数组去重 

##### 1、indexOf 循环去重 

##### 2、ES6 Set 去重；

Array.from(new Set(array))

#####  3、Object 键值对去重；

把数组的值存成 Object 的 key 值，比如 Object[value1] = true，在判断另一个值的时候，如果 Object[value2]存在的话， 就说明该值是重复的。

#### 问题2：之前说了 ES6set 可以数组去重，是否还有数组去重的方法 

法一：indexOf 循环去重 

法二：Object 键值对去重；把数组的值存成 Object 的 key 值，比如 Object[value1] = true，在判断另一个值的时候，如果 Object[value2]存在的话， 就说明该值是重复的。

### 2、闭包有什么用（或：来讲讲 JS 的闭包吧 ）

##### 1、什么是闭包

​	闭包是指有权访问另外一个函数作用域中的变量的函数。 闭包就是函数的局部变量集合，只是这些局部变量在函数返回后会继续存在。闭包就 是就是函数的“堆栈”在函数返回后并不释放，我们也可以理解为这些函数堆栈并不 在栈上分配而是在堆上分配。当在一个函数内定义另外一个函数就会产生闭包。

##### 2、为什么要用

​	 **匿名自执行函数**：我们知道所有的变量，如果不加上 var 关键字，则默认的会添加到 全局对象的属性上去，这样的临时变量加入全局对象有很多坏处，比如：别的函数可 能误用这些变量；造成全局对象过于庞大，影响访问速度(因为变量的取值是需要从原 型链上遍历的)。

​	除了每次使用变量都是用 var 关键字外，我们在实际情况下经常遇到 这样一种情况，即有的函数只需要执行一次，其内部变量无需维护，可以用闭包。 

​	结果缓存：我们开发中会碰到很多情况，设想我们有一个处理过程很耗时的函数对 象，每次调用都会花费很长时间，那么我们就需要将计算出来的值存储起来，当调用 这个函数的时候，首先在缓存中查找，如果找不到，则进行计算，然后更新缓存并返 回值，如果找到了，直接返回查找到的值即可。闭包正是可以做到这一点，因为它不 会释放外部的引用，从而函数内部的值可以得以保留。 

封装：实现类和继承等。

#### 问题2： 

### 3、事件代理在捕获阶段的实际应用

答：可以在父元素层面阻止事件向子元素传播，也可代替子元素执行某些操作。

### 4、去除字符串首尾空格 

答：使用正则(^\s*)|(\s*$)即可

### 5、性能优化

1、减少 HTTP 请求 

2、使用内容发布网络（CDN） 

3、添加本地缓存 压缩资源文件 

4、将 CSS 样式表放在顶部，把 javascript 放在底部（浏览器的运行机制决定） 

5、避免使用 CSS 表达式 

6、减少 DNS 查询 

7、使用外部 javascript 和 CSS 避免重定向 

8、图片 lazyLoad

### 6、能来讲讲 JS 的语言特性吗 

1、运行在客户端浏览器上； 

2、不用预编译，直接解析执行代码； 

3、是弱类型语言，较为灵活； 

4、与操作系统无关，跨平台的语言； 

5、脚本语言、解释性语言

### 7、如何判断一个数组(讲到 typeof 差点掉坑里) 

答：（1）Object.prototype.call.toString() ；（2）instanceof

### 8、你说到 typeof，能不能加一个限制条件达到判断条件 

答：typeof 只能判断是 object,可以判断一下是否拥有数组的方法

### 9、JS 实现跨域 

[前端常见跨域解决方案](https://segmentfault.com/a/1190000011145364)

##### 1、JSONP

通过动态创建 script，再请求一个带参网址实现跨域通信。document.domain + iframe 跨域：两个页面都通过 js 强制设置 document.domain 为基础主域，就实现了 同域。

##### 2、location.hash + iframe 跨域

a 欲与 b 跨域相互通信，通过中间页 c 来实现。 三个 页面，不同域之间利用 iframe 的 location.hash 传值，相同域之间直接 js 访问来通 信。 

##### 3、window.name + iframe 跨域

通过 iframe 的 src 属性由外域转向本地域，跨域数据即 由 iframe 的 window.name 从外域传递到本地域。

##### 4、postMessage 跨域

可以跨域操作的 window 属性之一。 

##### 5、CORS

服务端设置 Access-Control-Allow-Origin 即可，前端无须设置，若要带 cookie 请求，前后端都需要设置。 

##### 6、代理跨域

启一个代理服务器，实现数据的转发

#### 问题2：跨域的原理 

跨域，是指浏览器不能执行其他网站的脚本。它是由浏览器的同源策略造成的，是浏 览器对 JavaScript 实施的安全限制，那么只要协议、域名、端口有任何一个不同，都 被当作是不同的域。跨域原理，即是通过各种方式，避开浏览器的安全限制。

### 10、JS 基本数据类型 

答：基本数据类型：undefined、null、number、boolean、string、symbol

#### 问题2：不同数据类型的值的比较，是怎么转换的，有什么规则 

![image-20221108000811444](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221108000811444.png)

#### 问题3：null == undefined 为什么 

答：要比较相等性之前，不能将 null 和 undefined 转换成其他任何值，但 null == undefined 会返回 true 。ECMAScript 规范中是这样定义的

### 11、JS 的全排列 

```javascript
function permutate(str) {
	var result = [];
	if(str.length > 1) {
		var left = str[0];
		var rest = str.slice(1, str.length);
		var preResult = permutate(rest);
		for(var i=0; i<preResult.length; i++) {
			for(var j=0; j<preResult[i].length; j++) {
				var tmp = preResult[i],slice(0, j) + left + preResult[i].slice(j,
preResult[i].length);
				result.push(tmp);
			}
		}
	} else if (str.length == 1) {
		return [str];
	}
	return result;
}
```

### 12、暂停死区 

答：在代码块内，使用 let、const 命令声明变量之前，该变量都是不可用的。这在语法 上，称为“暂时性死区”。

### 13、有一个游戏叫做 Flappy Bird，就是一只小鸟在飞，前面是无尽的沙 漠，上下不断有钢管生成，你要躲避钢管。然后小明在玩这个游戏时候 老是卡顿甚至崩溃，说出原因（3-5 个）以及解决办法（3-5 个） 

##### 1、原因可能是

 1.内存溢出问题。 2.资源过大问题。 3.资源加载问题。 4.canvas 绘制频率问题

##### 2、解决方法

1.针对内存溢出问题，我们应该在钢管离开可视区域后，销毁钢管，让垃圾收集器回 收钢管，因为不断生成的钢管不及时清理容易导致内存溢出游戏崩溃。 

2.针对资源过大问题，我们应该选择图片文件大小更小的图片格式，比如使用 webp、 png 格式的图片，因为绘制图片需要较大计算量。 

3.针对资源加载问题，我们应该在可视区域之前就预加载好资源，如果在可视区域生 成钢管的话，用户的体验就认为钢管是卡顿后才生成的，不流畅。 

4.针对 canvas 绘制频率问题，我们应该需要知道大部分显示器刷新频率为 60 次/s,因 此游戏的每一帧绘制间隔时间需要小于 1000/60=16.7ms，才能让用户觉得不卡顿。 （注意因为这是单机游戏，所以回答与网络无关）

### 14、编写代码，满足以下条件： （1）Hero("37er");执行结果为 Hi! This is 37er （2）Hero("37er").kill(1).recover(30);执行结果为 Hi! This is 37er Kill 1 bug Recover 30 bloods （3） Hero("37er").sleep(10).kill(2)执行结果为 Hi! This is 37er //等 待 10s 后 Kill 2 bugs //注意为 bugs （双斜线后的为提示信息，不 需要打印）

```javascript
function Hero(name){
	let o=new Object();
	o.name=name;
	o.time=0;
	console.log("Hi! This is "+o.name);
	o.kill=function(bugs) {
		if(bugs==1){
		console.log("Kill "+(bugs)+" bug");
		}else {
            setTimeout(function () {
            console.log("Kill " + (bugs) + " bugs");
            }, 1000 * this.time);
        }
	return o;
};
o.recover=function (bloods) {
    console.log("Recover "+(bloods)+" bloods");
    return o;
}
o.sleep=function (sleepTime) {
    o.time=sleepTime;
    return o;
}
	return o;
}
```

### 15、说一下什么是 virtual dom 

答：用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树， 插到文档当中 当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树 进行比较，记录两棵树差异 把所记录的差异应用到所构建的真正的 DOM 树上，视图就 更新了。Virtual DOM 本质上就是在 JS 和 DOM 之间做了一个缓存

### 16、webpack 用来干什么的 

答:webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其 中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

### 17、ant-design 优点和缺点

优点：组件非常全面，样式效果也都比较不错。

缺点：框架自定义程度低，默认 UI 风格修改困难。

### 18、Vue 的生命周期 

1、**生命周期**：Vue 实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模板、挂载 Dom、渲染→更新→渲染、销毁等一系列过程，我们称这是 Vue 的生命周期。通俗说就 是 Vue 实例从创建到销毁的过程，就是生命周期。

2、每一个组件或者实例都会经历一个完整的生命周期，总共分为三个阶段：初始化、运 行中、销毁。

3、实例、组件通过 new Vue() 创建出来之后会初始化事件和生命周期，然后就会执行 beforeCreate 钩子函数，这个时候，数据还没有挂载呢，只是一个空壳，无法访问到 数据和真实的 dom，一般不做操作。

4、挂载数据，绑定事件等等，然后执行 created 函数，这个时候已经可以使用到数据， 也可以更改数据,在这里更改数据不会触发 updated 函数，在这里可以在渲染前倒数第 二次更改数据的机会，不会触发其他的钩子函数，一般可以在这里做初始数据的获取 接下来开始找实例或者组件对应的模板，编译模板为虚拟 dom 放入到 render 函数中准 备渲染，然后执行 beforeMount 钩子函数，在这个函数中虚拟 dom 已经创建完成，马 上就要渲染,在这里也可以更改数据，不会触发 updated，在这里可以在渲染前最后一 次更改数据的机会，不会触发其他的钩子函数，一般可以在这里做初始数据的获取 接下来开始 render，渲染出真实 dom，然后执行 mounted 钩子函数，此时，组件已经 出现在页面中，数据、真实 dom 都已经处理好了,事件都已经挂载好了，可以在这里操 作真实 dom 等事情...

5、当组件或实例的数据更改之后，会立即执行 beforeUpdate，然后 Vue 的虚拟 dom 机制 会重新构建虚拟 dom 与上一次的虚拟 dom 树利用 diff 算法进行对比之后重新渲染，一 般不做什么事儿

6、当更新完成后，执行 updated，数据已经更改完成，dom 也重新 render 完成，可以操 作更新后的虚拟 dom

7、当经过某种途径调用$destroy 方法后，立即执行 beforeDestroy，一般在这里做一些 善后工作，例如清除计时器、清除非指令绑定的事件等等 组件的数据绑定、监听...去掉后只剩下 dom 空壳，这个时候，执行 destroyed，在这 里做善后工作也可以

### 19、简单介绍一下 symbol 

Symbol 是 ES6 的新增属性，代表用给定名称作为唯一标识，这种类型的值可以这样创 建，let id=symbol(“id”)

Symbl 确保唯一，即使采用相同的名称，也会产生不同的值，我们创建一个字段，仅为 知道对应 symbol 的人能访问，使用 symbol 很有用，symbol 并不是 100%隐藏，有内置 方法 Object.getOwnPropertySymbols(obj)可以获得所有的 symbol。 也有一个方法 Reflect.ownKeys(obj)返回对象所有的键，包括 symbol。 所以并不是真正隐藏。但大多数库内置方法和语法结构遵循通用约定他们是隐藏的。
