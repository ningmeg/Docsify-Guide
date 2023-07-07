# fs 模块(异步)

fs 全称为<mark>file system</mark>，称之为<mark>文件系统</mark> ，是 Node.js 中的 内置模块 ，可以对计算机中的磁盘进行操作。

<mark>异步执行</mark> 是指主线程继续以上到下依次执行，而被设置为异步执行的代码会在另一个线程执行，主线程会跳过他，在另一个线程完成后直接输出(效率高)

## 一、使用 fs 模块

<mark>Node.js 提供了 exports 和 require 两个对象，其中 exports 是模块公开的接口，require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。</mark>

```javascript
const fs = require("fs");
// 标准引用fs模块，使用require引用
import { fs } from "fs";
// 使用ES6语法，引用fs模块
import * as fs from "fs";
// 对于默认导出，您应该使用：
```

## 二、文件写入

文件写入就是将 **数据** 保存到 **文件** 中，我们可以使用如下几个方法来实现该效果:

| 方法       | 说明     |
| ---------- | -------- |
| writeFile  | 异步写入 |
| appendFile | 追加写入 |
| readFile   | 异步读取 |

### 1-1 writeFile 异步写入

> 语法： fs.writeFile(file, data[, options], callback)  
> 参数说明：  
> file 文件名  
> data 待写入的数据  
> options 选项设置 （可选）  
> callback 写入回调  
> 返回值： undefined

代码示例:

```javascript
// require 是 Node.js 环境中的'全局'变量，用来导入模块
const fs = require('fs');
//将 『三人行，必有我师焉。』 写入到当前文件夹下的『座右铭.txt』文件中
fs.writeFile('./座右铭.txt', '三人行，必有我师焉。', err => {
//如果写入失败，则回调函数调用时，会传入错误对象，如写入成功，会传入 null
if(err){
console.log(err);
return;
}
console.log('写入成功')；
});
```

### 1-2 readFile 异步读取

> 语法： fs.readFile(path[, options], callback)  
> 参数说明：  
> path 文件路径  
> options 选项配置  
> callback 回调函数
> 返回值： undefined

代码示例：

```javascript
//导入 fs 模块

const fs = require("fs");
fs.readFile("./座右铭.txt", (err, data) => {
  if (err) throw err;
  console.log(data);
});
fs.readFile("./座右铭.txt", "utf-8", (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

### 1-3. appendFile 追加写入

appendFile 作用是在文件尾部追加内容，appendFile 语法与 writeFile 语法完全相同  
语法:

> fs.appendFile(file, data[, options], callback)  
> 返回值： undefined

实例代码：

```javascript
fs.appendFile("./座右铭.txt", "择其善者而从之，其不善者而改之。", (err) => {
  if (err) throw err;
  console.log("追加成功");
});
fs.appendFileSync("./座右铭.txt", "\r\n温故而知新, 可以为师矣");
```
