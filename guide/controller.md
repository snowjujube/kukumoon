# Controller - 控制器

## 创建控制器
```js
// app/controller/kukumoon.js
const { Controller } = require('@kukumoon/kukumoon-core');

class KukumoonController extends Controller {
    async query(ctx) {        
        const apps = await ctx.service.app.query();
        ctx.body = {
            apps,
        };
    }
}
module.exports = KukumoonController;
```
## 属性

| Property | 描述 |
| --- | --- |
| app | Kukumoon实例 |
| config | 应用配置 |

## 访问
可通过`app.controller.${Controller文件名的驼峰形式}`访问到对应的`Controller`实例。

通常只有路由文件才会访问`Controller`实例。