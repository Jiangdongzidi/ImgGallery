### 一、数据类型（8种）

Number, String，Boolean，NULL，Undefined，Object{arrary，function}，Bigint，Symbol

基本数据类型：Number，Boolean，String，undefined，Symbol

引用数据类型：Object

特殊的引用类型：

（1）null，指向空地址

（2）function：不用于鵆，所以没有赋值，拷贝函数一说。

### 二、引用数据类型和值类型

1、值类型变量：保存在**栈内存**中，属于深赋值。无法添加属性和方法

2、引用类型变量：变量名保存在**栈内存**，变量值保存在**堆内存**。不引用时，系统垃圾回收机制回收。属于浅赋值。可以添加属性和方法

### 三、虚值和真值

1、虚值（Falsy）：转换为Boolean值为false。真值（Truthy）：转换为Boolean值为true

虚值：长度为 0 的字符串，数字 0，false，undefined，null，NaN

真值：空数组，空对象，其他

### 四、JS数据类型判断

（一）typeof ——  无法区分对象、数组以及null

1、无法区分对象、数组以及null

```
let obj = {}
let arr = {}
let zs = null
console.log(typeof obj) // object
console.log(typeof arr) // object
console.log(typeof zs)  // object
```

![](E:\Learn\note\software_test_note\software_test_img\d70985cddf4a058420cec8e95656f625b9cc41bf.png)

2、Infinity 和 NaN 识别为 number。

```
let a = Infinity
let b = NaN
console.log(typeof a) // number
console.log(typeof b) // number
```

![](E:\Learn\note\software_test_note\software_test_img\6808c612b150b31d58f402b53ac95230b4951493.png)

3、识别所有值类型，识别函数类型

```
let a = 100
let b = 'hello'
let c = true
let d = Symbol('f')
let foo = () => {}
console.log(typeof a) // number
console.log(typeof b) // string
console.log(typeof c) // boolean
console.log(typeof d) //symbol
console.log(typeof foo) // function
```

![](E:\Learn\note\software_test_note\software_test_img\a940f6f29eafa4fde6e9a822b33b94809e9cba95.png)

（二）instanceof  ——  检测 null 和undefined 返回  undefined

1、检测所有new操作符创建的对象都返回true

2、检测  null  和  undefined  会返回  false

3、constructor

4、Object.prototype.toSring.call

5、空值null

6、未定义undefined

7、数字

8、数组
