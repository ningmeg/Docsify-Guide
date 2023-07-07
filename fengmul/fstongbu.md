# fs 模块(同步)

<mark>同步操作</mark>使用同步操作的话，他将不会获得另一个线程，代码会从上到下依次执行，如果遇到延时执行会等待它执行完成后，才执行。

## 一、文件写入

文件写入就是将 **数据** 保存到 **文件** 中，我们可以使用如下几个方法来实现该效果:

| 方法           | 说明     |
| -------------- | -------- |
| writeFileSync  | 同步写入 |
| appendFileSync | 追加写入 |
| readFileSync   | 同步读取 |

## 1-1. writeFileSync 同步写入

> 语法: fs.writeFileSync(file, data[, options])  
> 参数与 fs.writeFile 大体一致，只是没有 callback 参数  
> 返回值： undefined

代码示例：

```javascript
try {
  fs.writeFileSync("./座右铭.txt", "三人行，必有我师焉。");
} catch (e) {
  console.log(e);
}
```

> Node.js 中的磁盘操作是由其他 <mark>线程</mark> 完成的，结果的处理有两种模式：  
> 同步处理 JavaScript 主线程<mark>会等待</mark> 其他线程的执行结果，然后再继续执行主线程的代码,<mark>效率较低</mark>  
> 异步处理 JavaScript 主线程<mark>不会等待</mark>其他线程的执行结果，直接执行后续的主线程代码，<mark>效率较好</mark>

## 1-2. appendFileSync 追加写入

appendFile 作用是在文件尾部追加内容，appendFile 语法与 writeFile 语法完全相同
语法:

> fs.appendFileSync(file, data[, options])  
> 返回值： undefined

示例代码：

```javascript
try {
  fs.appendFileSync("./座右铭.txt", "择其善者而从之，其不善者而改之。");
} catch (e) {
  console.log(e);
}
```

## 1-3 readFileSync 同步读取

> 语法： fs.readFileSync(path[, options])  
> 参数说明：  
> path 文件路径  
> options 选项配置  
> 返回值： string | Buffer

代码示例：

```javascript
let data = fs.readFileSync("./座右铭.txt");
let data2 = fs.readFileSync("./座右铭.txt", "utf-8");
```
