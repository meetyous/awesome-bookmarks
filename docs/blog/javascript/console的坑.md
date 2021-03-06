## console.log 的坑

> 2018-09-18

console.log 应该是大部分程序员每天都没使用的函数，有时候觉得打断点太麻烦。但其实也是有一些小坑的。我们直接来举一个例子来看：

```js
const a = {}
console.log(a)
a.test = 1
console.log(a)

// 输出
// {test:1}
// {test:1}
```

大部分人会认为第一个输出的应该是一个空对象，是 a 对象的一个快照，但结果并不是这样的。
两次输出都是`{test:1}`。

同理数组

```js
const b = []
console.log(b)
b.push(1)
console.log(b)

// 输出
// [1]
// [1]
```

这就很明显了，在`console.log`一些复杂数据类型的时候，浏览器只是保存了一个引用而已，并不是打印执行时的结果。所以当你在控制台查看的时候是这个值经过了多次操作后，当前最终结果。所以打印复杂类型值的时候要注意一下，打印出来的值是不一定准确的。

但部分情况是问题不大的，当真遇到时就很蛋疼了，最简单的方法序列化一下`console.log(JSON.parse(JSON.stringify(obj)))`。其实就是深拷贝一下。
