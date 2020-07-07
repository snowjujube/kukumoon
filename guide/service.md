# Service - 业务逻辑

## 创建业务逻辑基类
```js
// app/service/app.js
const { Service } = require('@kukumoon/kukumoon-core');

class KukumoonService extends Service {
    async query() {
        return this.ctx.model.Kukumoon.findAll();
    }
}

module.exports = KukumoonService;
```

## 业务逻辑基类属性
| Property | 描述 |
| --- | --- |
| ctx | Koa Context |
| app | Kukumoon实例 |
| config | 应用配置 |

## 访问
可通过`ctx.service.${service文件名的驼峰形式}`访问到对应的`Service`实例。

举个例子，可通过`ctx.service.kukumoon`访问到上边定义的`app/service/kukumoon.js`文件中定义的`Service`类的实例。