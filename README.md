# 欢迎来到 Node.js 文档

## Node.js 简介

Node.js 是一个开源和跨平台的 JavaScript 运行时环境。 它几乎是任何类型项目的流行工具！

Node.js 在浏览器之外运行 V8 JavaScript 引擎（Google Chrome 的内核）。 这使得 Node.js 的性能非常好。

Node.js 应用程序在单个进程中运行，无需为每个请求创建新的线程。 Node.js 在其标准库中提供了一组异步的 I/O 原语，以防止 JavaScript 代码阻塞，通常，Node.js 中的库是使用非阻塞范式编写的，使得阻塞行为成为异常而不是常态。

当 Node.js 执行 I/O 操作时（比如从网络读取、访问数据库或文件系统），Node.js 将在响应返回时恢复操作（而不是阻塞线程和浪费 CPU 周期等待）。

这允许 Node.js 使用单个服务器处理数千个并发连接，而 ​​ 不会引入管理线程并发（这可能是错误的重要来源）的负担。

Node.js 具有独特的优势，因为数百万为浏览器编写 JavaScript 的前端开发者现在无需学习完全不同的语言，就可以编写除客户端代码之外的服务器端代码。

在 Node.js 中，可以毫无问题地使用新的 ECMAScript 标准，因为你不必等待所有用户更新他们的浏览器，你负责通过更改 Node.js 版本来决定使用哪个 ECMAScript 版本，你还可以通过运行带有标志的 Node.js 来启用特定的实验性功能。

## 大量的库

npm 以其简单的结构帮助 Node.js 生态系统蓬勃发展，现在 npm 仓库托管了超过 1,000,000 个开源包，你可以自由使用。

## npm 简单命令

```终端
node -v
//node版本

npm -v
//npm版本

npm
//查看 npm 命令列表

npm init
//创建模块

$ npm install npm@latest
//普通安装

$ npm install npm@latest -g
//-g 指以全局安装

npm list
//当前项目安装的所有模块

npm search <搜索词> [-g]
//用于搜索npm仓库，它后面可以跟字符串，也可以跟正则表达式。

npm uninstall
//卸载模块

 npm uninstall <name> [-g]
//卸载当前项目或全局模块

npm update <name>
//更新模块,可以后面加-g改为全局
```
