# 关于path.resolve的用法

关于Node里面的path.resolve()的用法，可以使用它来获取当前运行环境的文件路径，可以查看几个例子：

```javascript
const path = require('path');

console.log(__dirname);
console.log(path.resolve(__dirname));
console.log(path.resolve(__dirname, '../public'));
console.log(path.resolve(__dirname, './public'));
```

下面是运行的结果：

```javascript
E:\MyCode\Web\test\Node\resolve
E:\MyCode\Web\test\Node\resolve
E:\MyCode\Web\test\Node\public
E:\MyCode\Web\test\Node\resolve\public
```
可以看到，__dirname 获取当前运行文件 js 下的文件路径。<br />如果第二个参数含有 "../" 即可返回上一目录。由此我们可以拼接路径。<br />如果第二个参数是 "./"则是返回当前文件夹凭借路径。