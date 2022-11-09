# 面试题

### 1、对象深度克隆的简单实现

```javascript
function deepClone(obj){
	var newObj= obj instanceof Array ? []:{};
	for(var item in obj){
		var temple= typeof obj[item] == 'object' ?deepClone(obj[item]):obj[item];
		newObj[item] = temple;
	}
	return newObj;
}
```

ES5 的常用的对象克隆的一种方式。注意数组是对象，但是跟对象又有一定区别，所以 我们一开始判断了一些类型，决定 newObj 是对象还是数组。

#### 问题2：JS 深度拷贝一个元素的具体实现 

```javascript
var deepCopy = function(obj) {
	if (typeof obj !== 'object') return;
	var newObj = obj instanceof Array ? [] : {};
	for (var key in obj) {
		if (obj.hasOwnProperty(key)) {
			newObj[key] = typeof obj[key] === 'object' ? deepCopy(obj[key]) :
			obj[key];
		}
	}
	return newObj;
}
```

#### 问题3：写一个深度拷贝

```javascript
function clone( obj ) {
	var copy;
	switch( typeof obj ) {
		case "undefined":
			break;
		case "number":
			copy = obj - 0;
			break;
		case "string":
			copy = obj + "";
			break;
		case "boolean":
            copy = obj;
            break;
		case "object": //object 分为两种情况 对象（Object）和数组（Array）
            if(obj === null) {
            	copy = null;
            } else {
            	if( Object.prototype.toString.call(obj).slice(8, -1) === "Array") {
            		copy = [];
            		for( var i = 0 ; i < obj.length ; i++ ) {
            			copy.push(clone(obj[i]));
            		}
				} else {
                    copy = {};
                    for( var j in obj) {
                    	copy[j] = clone(obj[j]);
                  }
			}
		}
		break;
	default:
		copy = obj;
		break;
	}
	return copy;
}
```

### 2、实现一个 once 函数，传入函数参数只执行一次 

```javascript
function ones(func){
var tag=true;
return function(){
if(tag==true){
func.apply(null,arguments);
tag=false;
}
return undefined
}
}
```

### 3、将原生的 ajax 封装成 promise 

```javascript
var myNewAjax=function(url){
	return new Promise(function(resolve,reject){
		var xhr = new XMLHttpRequest();
		xhr.open('get',url);
		xhr.send(data);
		xhr.onreadystatechange=function(){
			if(xhr.status==200&&readyState==4){
				var json=JSON.parse(xhr.responseText);
				resolve(json)
			}else if(xhr.readyState==4&&xhr.status!=200){
				reject('error');
			}
		}
	})
}
```

### 4、 JS 监听对象属性的改变

我们假设这里有一个 user 对象, 

1、在 ES5 中可以通过 Object.defineProperty 来实现已有属性的监听

```javascript
Object.defineProperty(user,'name',{
	set：function(key,value){
	}
})
```

缺点：如果 id 不在 user 对象中，则不能监听 id 的变化

2、在 ES6 中可以通过 Proxy 来实现

```javascript
var user = new Proxy({}，{
	set：function(target,key,value,receiver){
	}
})
```

这样即使有属性在 user 中不存在，通过 user.id 来定义也同样可以这样监听这个属性 的变化哦。

### 5、如何实现一个私有变量，用 getName 方法可以访问，不能直接访问 

1、通过 defineProperty 来实现

```javascript
obj={
    name:yuxiaoliang,
    getName:function(){
    	return this.name
    }
}
object.defineProperty(obj,"name",{
//不可枚举不可配置
});
```

2、通过函数的创建形式

```javascript
function product(){
    var name='yuxiaoliang';
    this.getName=function(){
    	return name;
    }
}
var obj=new product();
```

### 6、==和===、以及 Object.is 的区别 

(1) == 主要存在：强制转换成 number,null==undefined

```javascript
" "==0 //true
"0"==0 //true
" " !="0" //true
123=="123" //true
null==undefined //true
```

(2)Object.js 主要的区别就是+0！=-0 而 NaN==NaN (相对比===和==的改进)

### 7、setTimeout、setInterval 和 requestAnimationFrame 之间的区别

#### 问题2：简历中提到了 requestAnimationFrame，请问是怎么使用的 

答：requestAnimationFrame() 方法告诉浏览器您希望执行动画并请求浏览器在下一次重 绘之前调用指定的函数来更新动画。该方法使用一个回调函数作为参数，这个回调函 数会在浏览器重绘之前调用。

### 8、实现一个两列等高布局，讲讲思路 

### 9、自己实现bind函数

原理：通过 apply 或者 call 方法来实现。

(1)初始版本

```javascript
Function.prototype.bind=function(obj,arg){
	var arg=Array.prototype.slice.call(arguments,1);
	var context=this;
	return function(newArg){
		arg=arg.concat(Array.prototype.slice.call(newArg));
		return context.apply(obj,arg);
	}
}
```

（2）考虑到原型链

为什么要考虑？因为在 new 一个 bind 过生成的新函数的时候，必须的条件是要继承原 函数的原型

```javascript
Function.prototype.bind=function(obj,arg){
	var arg=Array.prototype.slice.call(arguments,1);
	var context=this;
	var bound=function(newArg){
		arg=arg.concat(Array.prototype.slice.call(newArg));
		return context.apply(obj,arg);
		}
	var F=function(){}
	//这里需要一个寄生组合继承
	F.prototype=context.prototype;
	bound.prototype=new F();
	return bound;
}
```

### 10、用 setTimeout 来实现 setInterval

### 11、JS 怎么控制一次加载一张图片，加载完后再加载下一张

（1）方法一

```javascript
<script type="text/javascript">
    var obj=new Image();
    obj.src="http://www.phpernote.com/uploadfiles/editor/201107240502201179.jpg";
    obj.onload=function(){
    	alert('图片的宽度为：'+obj.width+'；图片的高度为：'+obj.height);
    	document.getElementById("mypic").innnerHTML="<img src='"+this.src+"'/>";
	}
</script>
<div id="mypic">onloading……</div>
```

（2）方法二

```javascript
<script type="text/javascript">
    var obj=new Image();
    obj.src="http://www.phpernote.com/uploadfiles/editor/201107240502201179.jpg";
    obj.onreadystatechange=function(){
        if(this.readyState=="complete"){
            alert('图片的宽度为：'+obj.width+'；图片的高度为：'+obj.height);
            document.getElementById("mypic").innnerHTML="<img src='"+this.src+"'/>";
        }
    }
</script>
<div id="mypic">onloading……</div>
```

#### 问题2：写一个函数，第一秒打印 1，第二秒打印 2 

##### 1、用 let 块级作用域

```javascript
for(let i=0;i<5;i++){
    setTimeout(function(){
    	console.log(i)
    },1000*i)
}
```

##### 2、闭包

```javascript
for(var i=0;i<5;i++){
    (function(i){
        setTimeout(function(){
        	console.log(i)
    	},1000*i)
    })(i)
}
```

### 12、代码执行顺序

```javascript
setTimeout(function(){
    console.log(1)},0);
	new Promise(function(resolve,reject){
		console.log(2);
		resolve();
		}).then(function(){console.log(3)
	}).then(function(){console.log(4)});
	process.nextTick(function(){console.log(5)});
	console.log(6);
//输出 2,6,5,3,4,1
```

[从promise、process.nextTick、setTimeout出发，谈谈Event Loop中的Job queue]: https://github.com/forthealllight/blog/issues/5

### 13、如何实现sleep的效果（es5或者es6）

##### (1)while 循环的方式

```javascript
function sleep(ms){
	var start=Date.now(),expire=start+ms;
	while(Date.now()<expire);
		console.log('1111');
	return;
}
```

执行 sleep(1000)之后，休眠了 1000ms 之后输出了 1111。上述循环的方式缺点很明 显，容易造成死循环。

##### (2)通过 promise 来实现

```javascript
function sleep(ms){
	var temple=new Promise(
		(resolve)=>{
		console.log(111);setTimeout(resolve,ms)
	});
	return temple
}
sleep(500).then(function(){
//console.log(222)
})
//先输出了 111，延迟 500ms 后输出 222
```

##### (3)通过 async 封装

```javascript
(3)通过 async 封装
function sleep(ms){
	return new Promise((resolve)=>setTimeout(resolve,ms));
}
async function test(){
	var temple=await sleep(1000);
	console.log(1111)
	return temple
}
test();
//延迟 1000ms 输出了 1111
```

##### (4).通过 generate 来实现

```javascript
function* sleep(ms){
	yield new Promise(function(resolve,reject){
		console.log(111);
		setTimeout(resolve,ms);
	})
}
sleep(500).next().value.then(function(){console.log(2222)})
```

### 14、简单实现一个promise

一般不会问的很详细，只要能写出上述文章中的 v1.0 版本的简单 promise 即可

### 15、Function._proto_(getPrototypeOf)是什么？

获取一个对象的原型，在 chrome 中可以通过_proto_的形式，或者在 ES6 中可以通过 Object.getPrototypeOf 的形式。 那么 Function.proto 是什么么？也就是说 Function 由什么对象继承而来，我们来做 如下判别。 

> Function.__ proto __==Object.prototype //false 
>
> Function.__ proto __==Function.prototype//true 

我们发现 Function 的原型也是 Function。 我们用图可以来明确这个关系：

![image-20221107224610539](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221107224610539.png)

### 16、实现 JS 中所有对象的深度克隆（包装对象，Date 对象，正则对象）

通过**递归**可以简单实现对象的深度克隆，但是这种方法不管是 ES6 还是 ES5 实现，都 有同样的缺陷，就是只能实现特定的 object 的深度复制（比如数组和函数），不能实现包装对象 Number，String ， Boolean，以及 Date 对象，RegExp 对象的复制。

### 17、简单实现 Node 的 Events 模块 

### 18、箭头函数中 this 指向举例 

```javascript
var a=11;
function test2(){
	this.a=22;
	let b=()=>{console.log(this.a)}
	b();
}
var x=new test2();
//输出 22
```

定义时绑定。

#### 问题2： this 的指向 哪几种

1、默认绑定：全局环境中，this 默认绑定到 window。 

2、隐式绑定：一般地，被直接对象所包含的函数调用时，也称为方法调用，this 隐式绑 定到该直接对象。

3、隐式丢失：隐式丢失是指被隐式绑定的函数丢失绑定对象，从而默认绑定到 window。

4、显式绑定：通过 call()、apply()、bind()方法把对象绑定到 this 上，叫做显式绑 定。 

5、new 绑定：如果函数或者方法调用之前带有关键字 new，它就构成构造函数调用。对于 this 绑定来说，称为 new 绑定。 

【1】构造函数通常不使用 return 关键字，它们通常初始化新对象，当构造函数的函 数体执行完毕时，它会显式返回。在这种情况下，构造函数调用表达式的计算结果就 是这个新对象的值。 

【2】如果构造函数使用 return 语句但没有指定返回值，或者返回一个原始值，那么 这时将忽略返回值，同时使用这个新对象作为调用结果。

【3】如果构造函数显式地使用 return 语句返回一个对象，那么调用表达式的值就是 这个对象。

### 19、JS判断类型

答：判断方法：typeof()，instanceof，Object.prototype.toString.call()等

### 20、数组常用方法 

答：push()，pop()，shift()，unshift()，splice()，sort()，reverse()，map()等

### 21、Vue 的生命周期 
