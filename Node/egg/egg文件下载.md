# egg.js 文件下载

话不多说，直接贴代码，参考官方示例：

```javascript
'use strict';
// 下载处理

const Controller = require('egg').Controller;
const path = require('path');
const fs = require('fs');

class DownloadController extends Controller {
  async download() {
    const filePath = path.resolve(this.app.config.static.dir, 'hello.txt');
    console.log(this.app.config.static.dir);
    this.ctx.attachment('hello.txt');
    this.ctx.body = fs.createReadStream(filePath);
  }
}

module.exports = DownloadController;

```

记得在 public 文件夹下方上文件：

roter.js

```javascript
'use strict';

/**
 * @param {Egg.Application} app - egg application
 */
module.exports = app => {
  const { router, controller } = app;
  router.get('/', controller.home.index);
  router.get('/test', controller.test.index);
  router.post('/upload', controller.fileUpload.upload);
  router.get('/download', controller.download.download);
};

```

官方示例代码：<br />[https://github.com/eggjs/examples/blob/master/download/app/controller/index.js](https://github.com/eggjs/examples/blob/master/download/app/controller/index.js)