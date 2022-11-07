# 面试题

### 1、对象深度克隆的简单实现

```javascript
function deepClone(obj){
var newObj= obj instanceof Array ? []:{};
for(var item in obj){
var temple= typeof obj[item] == 'object' ?
deepClone(obj[item]):obj[item];
newObj[item] = temple;
}
return newObj;
}
```

ES5 的常用的对象克隆的一种方式。注意数组是对象，但是跟对象又有一定区别，所以 我们一开始判断了一些类型，决定 newObj 是对象还是数组。

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
obj.src="http://www.phpernote.com/uploadfiles/editor/2011072405022011
79.jpg";
obj.onload=function(){
alert('图片的宽度为：'+obj.width+'；图片的高度为：'+obj.height);
document.getElementById("mypic").innnerHTML="<img src='"+this.src+"'
/>";
}
</script>
<div id="mypic">onloading……</div>
```

（2）方法二

```javascript
<script type="text/javascript">
var obj=new Image();
obj.src="http://www.phpernote.com/uploadfiles/editor/2011072405022011
79.jpg";
obj.onreadystatechange=function(){
if(this.readyState=="complete"){
alert('图片的宽度为：'+obj.width+'；图片的高度为：'+obj.height);
document.getElementById("mypic").innnerHTML="<img src='"+this.src+"'
/>";
}
}
</script>
<div id="mypic">onloading……</div>
```

### 12、代码执行顺序

```javascript
setTimeout(function(){console.log(1)},0);
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

