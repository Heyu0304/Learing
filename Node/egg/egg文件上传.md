# egg.js 文件上传

首先安装包：

```javascript
npm install await-stream-ready stream-wormhole dayjs
```

在config下面的config.default.js配置相关下载信息：


```javascript
config.multipart = {
    fileSize: '50mb',
    mode: 'stream', // 这里要配置成stream，详情可以参考官网。俩个模式。
  };

  config.security = {
    csrf: {
      enable: false,
    },
  };
```

下面是代码块：

```javascript
'use strict';

const Controller = require('egg').Controller;
const fs = require('fs');
const path = require('path');
const sendToWormhole = require('stream-wormhole');
const awaitWriteStream = require('await-stream-ready').write;

class FileUploadController extends Controller {
  async upload() {
    const { ctx } = this;
    
    const stream = await ctx.getFileStream();
    const name = Date.now() + '' + path.extname(stream.filename).toLocaleLowerCase(); // 获取文件的尾缀名（扩展名）
    console.log('name:>>>>>>>', name);
    console.log('filename:>>>>>>>', stream.filename);

    const target = path.resolve(__dirname, '../uploads'); // 保存的文件夹路径

    // 判断存储的文件夹是否存在，不存在则创建
    if (!fs.existsSync(target)) {
      fs.mkdirSync(target);
    }

    const targetFilename = path.join(target, name); // 写入的文件名称, 目标文件名
    console.log('filename:>>>>>>>', targetFilename);

    const writeStream = fs.createWriteStream(targetFilename);

    try {
      await awaitWriteStream(stream.pipe(writeStream));
    } catch (e) {
      await sendToWormhole(stream);
      console.log(e);
      throw e;
    }
    ctx.body = {
      code: 200,
      message: '上传成功',
      data: stream.filename,
    };
  }
}

module.exports = FileUploadController;

```

然后配置相关路由信息：

```javascript
router.post('/upload', controller.fileUpload.upload);
```

关键点：<br />1、要配置 csrf 设置为false，否则会报错。<br />2、要判断文件夹是否存在，不存在就存储写入会报错。之前的方法，fs.exits()这个方法已经被放弃了，要注意。<br />3、要熟悉path.resolve()的使用，path.resolve(__dirname, '../uploads') 会返回文件存储路径。<br />4、awaitWriteStream 和 sendToWormhole 是在网上看到关于异步存储文件的方法。<br />5、文件操作的话，这里用的流，stream，知识点薄弱的建议多看看文件系统知识。