# jwt生成token

### 1、下载jwt —— 生成token

`npm i jwt-simple --save-dev`

![image-20221110111253902](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221110111253902.png)

### 2、在controller/account.js中引入jwt

```
const jwt = require("jwt-simple")
```

![image-20221111105207009](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221111105207009.png)

### 3、在config/index.js中添加  `tokenKey: "youker.net"`

```javascript
tokenKey: "youker.net"
```

![image-20221110111945422](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221110111945422.png)

### 4、在controller/account.js中创建createToken，并登录成功后返回值添加token

![image-20221110112022679](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221110112022679.png)

**controller/account.js**

```javascript
const db = require("../core/mysql");
// moment  时间
const moment = require("moment")
// 加密 : 注册时密码加密
const md5 = require("md5")
// json web token
const jwt = require("jwt-simple")

class AccountController {
    // 注册
    async register (request, resposne, next) {
        let insertSql = 'insert into users (u_name, u_pwd, u_sex, u_create) values (?,?,?,?);';
        let params = [
            request.body.name,
            // md5加密
            md5(request.body.pwd + require("../config").key),
            // request.body.pwd,
            request.body.sex == undefined ? '男' : request.body.sex,
            // request.body.sex == '' ? '男' : request.body.sex,
            moment().format('YYYY-MM-DD HH:mm:ss')
        ];

        // exec : 连接数据库，执行sql语句。返回promise，可以使用await/async
        // let result = await db.exec(insertSql, params);

        try {
            let result = await db.exec(insertSql, params);
            if (result && result.affectedRows >= 1) {
                resposne.json({
                    code: 200,
                    msg: "注册成功"
                })
            } else {
                resposne.json({
                    code: 200,
                    msg: "注册失败"
                })
            }
        } catch (error) {
            resposne.json({
                code: -200,
                msg: "服务器异常",
                error
            })
            
        }
    }

    // 登录
    async login (request, resposne, next) {
        let loginSql = 'select u_id, u_name, u_sex ,u_create from users where u_name = ? and u_pwd = ? and u_status = 1;';
        let params = [
            request.body.name,
            // md5的二次加密
            md5(request.body.pwd + require("../config").key),
            // md5(request.body.pwd)
        ]
        try {
            let result = await db.exec(loginSql, params);
            if (result && result.length >= 1) {
                resposne.json({
                    code: 200,
                    msg: "登录成功",
                    data: result[0],
                    // 登录成功返回一个token
                    token: createToken(result[0])
                })
            } else {
                resposne.json({
                    code: 200,
                    msg: "登录失败",
                    data: result[0]
                })
            }
        } catch (error) {
            resposne.json({
                code: 200,
                msg: "登录失败",
                data: result[0],
                error
            })     
        }
        function createToken(data) {
            return jwt.encode({
                exp: Date.now() + (1000 * 60 *60 * 24),
                info: data
            }, require("../config").tokenKey)
        }
    }

    
}

module.exports = new AccountController();
```

### 6、测试login和register接口生成token

![image-20221111111316552](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221111111316552.png)

![image-20221111124856753](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221111124856753.png)



![](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221111104318864.png)

### 7、路由token拦截

![image-20221111231035993](https://typora-bucket21.oss-cn-guangzhou.aliyuncs.com/note_images/image-20221111231035993.png)

```javascript
const jwt = require("jwt-simple");
const express = require("express");
let router = express.Router();

// 需要token 拦截， 如果带了token，才能让你访问以下4个接口
// 前端需要发送token
router.use((request, resposne, next) => {
    // 前端携带数据到后台，有哪些方式？ 返回数据中有token
    if (request.body.token || request.query.token || request.headers.token || request.cookies.token) {
        
        // 进行解密
        try {
            let token = request.body.token || request.query.token || request.headers.token || request.cookies.token;
            let result = jwt.decode(token, require("../config").tokenKey)
            if (result) {
                // result 是对象
                next();
            }
        } catch (error) {
            resposne.json({
                code: -200,
                msg: "token失效，请重新登录"
            })
        }
    }

    next();
})
router.get("/getCart", require("../controller/carts").getCartByUser);
router.get("/delete", require("../controller/carts").deleteCart);
router.get("/modify", require("../controller/carts").modifyCart);
router.get("/add", require("../controller/carts").addCart);
router.get("/giveMony", require("../controller/carts").giveMony);

// 暴露
module.exports = router;
```

