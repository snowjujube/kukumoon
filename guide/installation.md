# 快速上手

> 本文将从实例的角度，一步步地搭建出一个 Kukumoon 应用，让你能快速的上手 Kukumoon。

## 环境要求

操作系统：支持 macOS，Linux，Windows
运行环境：建议选择 LTS 版本，最低要求 8.x。

## 使用脚手架初始化项目

还未支持

你也可以选择直接clone一份现成的示例应用：

```shell script
$ git clone https://github.com/snowjujube/kukumoon-demo
$ cd kukumoon-demo && npm install
```

记得启动项目：

```shell script
$ npm run dev
```

## 编写Controller
如果你熟悉 `Web` 开发或 `MVC`，肯定猜到我们第一步需要编写的是 `Controller` 和 `Router`。

```js
// app/controller/kukumoon.js
const { Controller } = require('@kukumoon/kukumoon-core');

class KukumoonController extends Controller {
    async query(ctx) {        
        const apps = await Promise.resolve('apps information');
        ctx.body = {
            apps,
        };
    }
}
module.exports = KukumoonController;
```

编写路由：

```js
// app/router.js
module.exports = app => {
  const { router, controller } = app;
  router.get('/', controller.kukumoon.query);
};
```

## 编写Service

在实际应用中，`Controller` 一般不会自己产出数据，也不会包含复杂的逻辑，复杂的过程应抽象为业务逻辑层 `Service`。

我们来编写一个`Service`将业务逻辑接管过来：

```js
// app/service/app.js
const { Service } = require('kukumoon/kukumoon-core');

class KukumoonService extends Service {
    async query() {
        return 'apps information';
    }
}

module.exports = KukumoonService;
```

记得在刚刚编写好的`Controller`中调用新的`Service`：

```js
// app/controller/kukumoon.js
const { Controller } = require('kukumoon/kukumoon-core');

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

至此，我们便完成了一个最基本的`Kukumoon`应用！恭喜你🎉！