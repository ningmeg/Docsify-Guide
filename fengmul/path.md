# path 模块

path 模块提供了<mark> 操作路径 </mark>的功能，我们将介绍如下几个较为常用的几个 API：

| API           | 说明                                 |
| ------------- | ------------------------------------ |
| path.resolve  | 拼接规范的绝对路径<mark> 常用</mark> |
| path.sep      | 获取操作系统的路径分隔符             |
| path.parse    | 解析路径并返回对象                   |
| path.basename | 获取路径的基础名称                   |
| path.dirname  | 获取路径的目录名                     |
| path.extname  | 获得路径的扩展名                     |

代码示例：

```javascript
const path = require("path");
//获取路径分隔符
console.log(path.sep);
//拼接绝对路径
console.log(path.resolve(__dirname, "test"));
//解析路径
let pathname = "D:/program file/nodejs/node.exe";
console.log(path.parse(pathname));
//获取路径基础名称
console.log(path.basename(pathname));
//获取路径的目录名
console.log(path.dirname(pathname));
//获取路径的扩展名
console.log(path.extname(pathname));
```

## Windows 与 POSIX 的对比

node:path 模块的默认操作因运行 Node.js 应用程序的操作系统而异。 具体来说，当在 Windows 操作系统上运行时，node:path 模块将假定正在使用 Windows 风格的路径。

因此，在 POSIX 和 Windows 上使用 path.basename() 可能会产生不同的结果：

在 POSIX 上：

```javascript
path.basename("C:\\temp\\myfile.html");
// 返回: 'C:\\temp\\myfile.html'
```

在 Windows 上：

```javascript
path.basename("C:\\temp\\myfile.html");
// 返回: 'myfile.html'
```

当使用 Windows 文件路径时，若要在任何操作系统上获得一致的结果，则使用 path.win32：

在 POSIX 和 Windows 上：

```javascript
path.win32.basename("C:\\temp\\myfile.html");
// 返回: 'myfile.html'
```

当使用 POSIX 文件路径时，若要在任何操作系统上获得一致的结果，则使用 path.posix：

在 POSIX 和 Windows 上：

```javascript
path.posix.basename("/tmp/myfile.html");
// 返回: 'myfile.html'
```

在 Windows 上，Node.js 遵循独立驱动器工作目录的概念。 当使用不带反斜杠的驱动器路径时，可以观察到此行为。 例如，<mark>path.resolve('C:\\')</mark> 可能返回与<mark>path.resolve('C:')</mark>不同的结果。 有关详细信息，请参阅此 MSDN 页面。
