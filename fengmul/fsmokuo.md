# fs 模块

## 1-1 createWriteStream 流式写入

> 语法： fs.createWriteStream(path[, options])  
> 参数说明：  
> path 文件路径  
> options 选项配置（ 可选 ）  
> 返回值： Object

代码示例：

```javascript
let ws = fs.createWriteStream("./观书有感.txt");
ws.write("半亩方塘一鉴开\r\n");
ws.write("天光云影共徘徊\r\n");
ws.write("问渠那得清如许\r\n");
ws.write("为有源头活水来\r\n");
ws.end();
```

> 程序打开一个文件是需要消耗资源的 ，流式写入可以减少打开关闭文件的次数。  
> 流式写入方式适用于 大文件写入或者频繁写入的场景,writeFile 适合于 写入频率较低的场景

## 1.2 createReadStream 流式读取

> 语法： fs.createReadStream(path[, options])  
> 参数说明：  
> path 文件路径  
> options 选项配置（ 可选 ）  
> 返回值： Object

代码示例：

```javascript
//创建读取流对象
let rs = fs.createReadStream("./观书有感.txt");
//每次取出 64k 数据后执行一次 data 回调
rs.on("data", (data) => {
  console.log(data);
  console.log(data.length);
});
//读取完毕后, 执行 end 回调
rs.on("end", () => {
  console.log("读取完成");
});
```

## 1.3 文件移动与重命名

在 Node.js 中，我们可以使用 <mark>rename</mark> 或<mark>renameSync</mark> 来移动或重命名<mark>文件或文件夹</mark>

> 语法：  
> fs.rename(oldPath, newPath, callback)  
> fs.renameSync(oldPath, newPath)  
> 参数说明：  
> oldPath 文件当前的路径  
> newPath 文件新的路径  
> callback 操作后的回调  
> 代码示例：

```javascript
//创建读取流对象
let rs = fs.createReadStream("./观书有感.txt");
//每次取出 64k 数据后执行一次 data 回调
rs.on("data", (data) => {
  console.log(data);
  console.log(data.length);
});
//读取完毕后, 执行 end 回调
rs.on("end", () => {
  console.log("读取完成");
});
fs.rename("./观书有感.txt", "./论语/观书有感.txt", (err) => {
  if (err) throw err;
  console.log("移动完成");
});
fs.renameSync("./座右铭.txt", "./论语/我的座右铭.txt");
```

## 1.4 文件删除

在 Node.js 中，我们可以使用<mark>unlink</mark>或<mark>unlinkSync</mark>来删除文件

> 语法：  
> fs.unlink(path, callback)  
> fs.unlinkSync(path)  
> 参数说明：  
> path 文件路径  
> callback 操作后的回调

代码示例：

```javascript
const fs = require("fs");
fs.unlink("./test.txt", (err) => {
  if (err) throw err;
  console.log("删除成功");
});
fs.unlinkSync("./test2.txt");
```

## 二、文件夹操作

借助 Node.js 的能力，我们可以对文件夹进行 创建 、 读取 、 删除 等操作

<mark>注意：后面带有 Sync 的是同步方法,默认是异步操作</mark>

| 方法                  | 说明       |
| --------------------- | ---------- |
| mkdir / mkdirSync     | 创建文件夹 |
| readdir / readdirSync | 读取文件夹 |
| rmdir / rmdirSync     | 删除文件夹 |

### 2-1 mkdir 创建文件夹

在 Node.js 中，我们可以使用 <mark>mkdir </mark>或 <mark>mkdirSync</mark> 来创建文件夹

> 语法：  
> fs.mkdir(path[, options], callback)  
> fs.mkdirSync(path[, options])  
> 参数说明：  
> path 文件夹路径  
> options 选项配置（ 可选 ）  
> callback 操作后的回调

示例代码：

```javascript
//异步创建文件夹
fs.mkdir("./page", (err) => {
  if (err) throw err;
  console.log("创建成功");
});
//递归异步创建
fs.mkdir("./1/2/3", { recursive: true }, (err) => {
  if (err) throw err;
  console.log("递归创建成功");
});
//递归同步创建文件夹
fs.mkdirSync("./x/y/z", { recursive: true });
```

### 2-2 readdir 读取文件夹

在 Node.js 中，我们可以使用 <mark>readdir </mark>或 <mark>readdirSync</mark> 来读取文件夹

> 语法：  
> fs.readdir(path[, options], callback)  
> fs.readdirSync(path[, options])  
> 参数说明：  
> path 文件夹路径  
> options 选项配置（ 可选 ）  
> callback 操作后的回调

示例代码：

```javascript
//异步读取
fs.readdir("./论语", (err, data) => {
  if (err) throw err;
  console.log(data);
});
//同步读取
let data = fs.readdirSync("./论语");
console.log(data);
```

### 2-3 rmdir 删除文件夹

在 Node.js 中，我们可以使用 <mark>rmdir</mark> 或 <mark>rmdirSync</mark> 来删除文件夹

> 语法：  
> fs.rmdir(path[, options], callback)  
> fs.rmdirSync(path[, options])  
> 参数说明：  
> path 文件夹路径  
> options 选项配置（ 可选 ）  
> callback 操作后的回调

示例代码：

```javascript
//异步删除文件夹
fs.rmdir("./page", (err) => {
  if (err) throw err;
  console.log("删除成功");
});
//异步递归删除文件夹
fs.rmdir("./1", { recursive: true }, (err) => {
  if (err) {
    console.log(err);
  }
  console.log("递归删除");
});
//同步递归删除文件夹
fs.rmdirSync("./x", { recursive: true });
```

## 三、查看资源状态

在 Node.js 中，我们可以使用 <mark>stat </mark>或 <mark>statSync </mark>来查看资源的详细信息

> 语法：  
> fs.stat(path[, options], callback)  
> fs.statSync(path[, options])  
> 参数说明：  
> path 文件夹路径  
> options 选项配置（ 可选 ）  
> callback 操作后的回调

示例代码：

```javascript
//异步获取状态
fs.stat("./data.txt", (err, data) => {
  if (err) throw err;
  console.log(data);
});
//同步获取状态
let data = fs.statSync("./data.txt");
```

结果值对象结构：

> size 文件体积  
> birthtime 创建时间  
> mtime 最后修改时间  
> isFile 检测是否为文件  
> isDirectory 检测是否为文件夹

## 四.fs 模块进阶（readline 模块）

### 4.1 介绍

> 在 Node.js 中，由于其运行在服务端环境，无法直接弹出浏览器的对话框，但是可以通过一些外部库实现类似的功能。  
> 可以使用 readline 模块来读取用户的输入，然后根据用户的选择来决定

### 4.2 引用

readline 模块是 Node.js 的一个内置模块，可以直接通过 require('readline')来使用。这个模块提供了一些工具，用于从可读流（例如标准输入流）中逐行读取数据。

readline 模块提供了 createInterface() 方法，用于创建一个 Interface 对象。通过这个对象，我们可以逐行读取数据、输出提示信息，并在用户输入后触发回调函数。

```javascript
const readline = require("readline");
```

简单使用

```javascript
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

rl.setPrompt("请输入一个字符串> ");
rl.prompt();

rl.on("line", (input) => {
  if (input === "exit") {
    console.log("程序结束");
    rl.close();
  } else {
    console.log(`您输入的是：${input}`);
    rl.prompt();
  }
});
```

> 在上面的代码中，我们首先使用 createInterface() 方法创建了一个 Interface 对象，并指定了输入流和输出流。然后使用 setPrompt() 方法设置了提示信息，在 prompt() 方法中输出这个提示信息。

> 接着，我们监听了 line 事件，当用户输入一行数据后就会触发这个事件。在事件处理函数中，我们判断用户输入的内容，如果是 exit 就结束程序，否则就输出输入的字符串，并再次调用 prompt() 方法等待用户输入。当用户输入 exit 并触发了 close 事件后，程序就会结束。

### 4.3 使用

```javascript
const readline = require("readline");
const fs = require("fs");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

rl.question("是否创建文件？（y/n）", (answer) => {
  if (answer === "y") {
    fs.writeFile("./test.txt", "Hello World", (err) => {
      if (err) {
        console.error("创建文件失败：", err);
      } else {
        console.log("文件创建成功！");
      }
    });
  } else {
    console.log("不创建文件。");
  }

  rl.close();
});
```

> 在这个示例中，我们使用 readline 模块创建了一个用户输入的接口，并向用户询问是否创建文件。根据用户的输入，如果用户输入了 y，则使用 fs.writeFile 方法创建文件，否则不进行任何操作。  
> 注意，使用 readline 模块读取用户的输入是一个异步操作，需要在回调函数中进行相应的处理。同时，在使用完 readline 接口后，需要通过调用 close 方法来关闭该接口。

process.stdin 是 Node.js 中的一个全局对象，它是一个可读流（Readable Stream），用于从标准输入中读取用户输入的数据。

在命令行中运行 Node.js 程序时，可以通过键盘输入来向程序发送数据。process.stdin 对象就是用于读取这些输入数据的对象。

```javascript
process.stdin.on("data", (data) => {
  console.log(`你输入了：${data.toString().trim()}`);
});
```

> 由于输入数据可能会包含换行符等特殊字符，因此需要通过 toString() 方法将输入数据转换为字符串，并使用 trim() 方法将字符串两端的空格删除。

process.stdout 是 Node.js 中的一个全局对象，它是一个可写流（Writable Stream），用于向标准输出中写入数据。

在命令行中运行 Node.js 程序时，程序可以通过 console.log() 等方法将数据输出到控制台。这些输出数据实际上是通过 process.stdout 对象向标准输出流中写入的。

```javascript
process.stdout.write("Hello, world!\n");
```

需要注意的是，process.stdout 对象是一个可写流，写入数据是异步操作，因此写入数据后不一定会立即被输出。如果需要在写入数据后执行一些操作，可以监听 drain 事件，该事件在可写流的缓冲区已经被清空时触发。

```javascript
process.stdout.write("Hello, world!\n", () => {
  console.log("数据已经写入");
});
process.stdout.on("drain", () => {
  console.log("缓冲区已经被清空");
});
```

### rl.question()

rl.question() 是 readline 模块中一个比较常用的方法，用于向用户提问并等待用户的回答。这个方法会将问题和一个回调函数作为参数传入，当用户输入回答后，回调函数会被触发，回调函数的参数就是用户的回答。

rl.question() 的语法如下：

```javascript
rl.question(query, callback);
```

其中，query 是一个字符串，表示要向用户询问的问题；callback 是一个函数，当用户输入回答后，会调用这个函数，并将用户的回答作为参数传入。回调函数的第一个参数就是用户的回答。

例如，下面的代码向用户询问一个问题，当用户输入回答后，将回答输出到控制台：

```javascript
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

rl.question("请输入一个字符串> ", (answer) => {
  console.log(`您输入的是：${answer}`);
  rl.close();
});
```

> 在上面的代码中，我们使用 rl.question() 方法向用户询问一个问题，问题的提示信息为 '请输入一个字符串> '。当用户输入回答后，回调函数会被触发，并将用户的回答作为参数传入，我们在回调函数中将回答输出到控制台，并使用 rl.close() 方法关闭 Interface 对象，结束程序的执行。

>需要注意的是，rl.question() 方法只能被调用一次。如果你想要多次向用户提问，可以使用 rl.setPrompt() 方法设置提示信息，并通过 rl.prompt() 方法输出提示信息，然后通过监听 line 事件来获取用户的输入。

### 4.4 例子

这是 fs 模块和 readline 模块使用

```javascript
const fs = require("fs");
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

const aa = {
  data: "",
};

rl.question("你要查找的文件/文件夹", (answer) => {
  if (!answer) {
    console.log("输入不能为空！");
  } else {
    console.log(`您输入的是：${answer.trim()}`);
    aa.data = answer.trim();
    wenjian();
  }
});

function wenjian() {
  console.log("./ceshi/" + aa.data);
  fs.readdir("./ceshi", (err, data) => {
    if (err) throw err;
    console.log(data);

    fs.stat("./ceshi/" + aa.data, (err, stats) => {
      if (err) {
        console.error("获取文件信息失败：", err);
        console.log("你可能没有这个文件夹");
        rl.question("是否创建文件", (answer) => {
          console.log(`您输入的是：${answer}`);
          if (
            answer.trim() == "yes" ||
            answer.trim() == "是" ||
            answer.trim() == "y"
          ) {
            fs.mkdir("./ceshi/" + aa.data, (err) => {
              if (err) throw err;
              console.log("创建成功");
            });
          } else {
            console.log("退出");
          }
          rl.close();
        });
      } else {
        console.log("文件类型：", stats.isFile() ? "文件" : "文件夹");
        console.log("文件大小：", stats.size);
        console.log("文件权限：", stats.mode);
      }
    });
  });
  rl.close();
}
```

## 五、总结

> fs.access(): 检查文件是否存在，以及 Node.js 是否有权限访问。  
> fs.appendFile(): 追加数据到文件。如果文件不存在，则创建文件。  
> fs.chmod(): 更改文件（通过传入的文件名指定）的权限。相关方法：fs.lchmod()、fs.fchmod()。  
> fs.chown(): 更改文件（通过传入的文件名指定）的所有者和群组。相关方法：fs.fchown()、fs.lchown()。  
> fs.close(): 关闭文件描述符。  
> fs.copyFile(): 拷贝文件。  
> fs.createReadStream(): 创建可读的文件流。  
> fs.createWriteStream(): 创建可写的文件流。  
> fs.link(): 新建指向文件的硬链接。    
> fs.mkdir(): 新建文件夹。  
> fs.mkdtemp(): 创建临时目录。    
> fs.open(): 设置文件模式。  
> fs.readdir(): 读取目录的内容。  
> fs.readFile(): 读取文件的内容。相关方法：fs.read()。  
> fs.readlink(): 读取符号链接的值。   
> fs.realpath(): 将相对的文件路径指针（.、..）解析为完整的路径。  
> fs.rename(): 重命名文件或文件夹。  
> fs.rmdir(): 删除文件夹。  
> fs.stat(): 返回文件（通过传入的文件名指定）的状态。相关方法：fs.fstat()、fs. lstat()。  
> fs.symlink(): 新建文件的符号链接。  
> fs.truncate(): 将传递的文件名标识的文件截断为指定的长度。相关方法：fs.ftruncate()。  
> fs.unlink(): 删除文件或符号链接。  
> fs.unwatchFile(): 停止监视文件上的更改。  
> fs.utimes(): 更改文件（通过传入的文件名指定）的时间戳。相关方法：fs.futim()。  
> fs.watchFile(): 开始监视文件上的更改。相关方法：fs.watch()。  
> fs.writeFile(): 将数据写入文件。相关方法：fs.write()。  

关于 fs 模块的特殊之处是，所有的方法默认情况下都是异步的，但是通过在前面加上 Sync 也可以同步地工作。

例如：

> fs.rename()  
> fs.renameSync()  
> fs.write()  
> fs.writeSync()

这在应用程序流程中会产生巨大的差异。

例如，试验一下 fs.rename() 方法。 异步的 API 会与回调一起使用：

```javascript
const fs = require("fs");

fs.rename("before.json", "after.json", (err) => {
  if (err) {
    return console.error(err);
  }

  //完成
});
```

同步的 API 则可以这样使用，并使用 try/catch 块来处理错误：

```javascript
const fs = require("fs");

try {
  fs.renameSync("before.json", "after.json");
  //完成
} catch (err) {
  console.error(err);
}
```

此处的主要区别在于，在第二个示例中，脚本的执行会阻塞，直到文件操作成功。
