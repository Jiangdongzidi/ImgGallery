一、resolve 和 reject

1、执行了 resolve ， Promise状态会变成 fulfilled

2、执行了  reject，Promise状态会变成 rejected

3、Promise 只以第一次为准，第一次成功就永久为 fulfilled，第一次失败就永久为  rejected

4、Promise 中有  throw  的话，就相当于执行了 reject

5、Promise 的初始状态 pending

二、throw

三、then

（一）then实现

1、then  接收两个回调，一个是**成功回调**，一个是**失败回调**

2、当 Promise 状态为 fulilled 执行 成功回调， 为  rejected  执行失败回调

3、如  resolve 或 reject 在定时器里，则定时器结束后再执行 then

4、then  支持链式调用，下次  then  执行收上一次  then  返回值的影响

（二）then的链式调用

**then支持`链式调用`，下一次then执行`受上一次then返回值的影响`**

1、**then  方法本身会返回一个新的  Promise  对象**

2、如果返回值是  Promise  对象，返回值为成功，新promise就是成功

3、如果返回值是  promise  对象， 返回值为失败，新promise就是失败

4、如果返回值废  promise  对象，新promise对象就是成功，值为此返回值
