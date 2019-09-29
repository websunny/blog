# node中流（Stream）的理解

## 什么是流？

> node官方文档上是这么描述的：流（stream）是一种在 Node.js 中处理流式数据的抽象接口

额，果然是很抽象，其实简单的理解就是node用来处理数据的一个工具。

## 为什么需要使用流？

我们在使用node的过程中，不可避免的需要对数据进行处理，对此node一般有两种处理模式，一种是buffer模式，另外一种就是本文提到的stream模式。

两者的区别在于，处理数据时buffer会将数据先存储在内存中，继而对内存进行操作。而流模式则是边读数据边进行处理。

因此无论是在空间还是时间两个角度，流模式都远远优于buffer模式。

```js
const fs = require('fs');

fs.readFile(file, function (err, body) {

        console.log(body);

        console.log(body.toString());

})
```

当我们在读取大文件类似视频时，使用buffer模式就可能会报错，愿意是buffer对象过于庞大，toString方法失败。这时候就应当使用流模块进行处理。

```js
const fs = require('fs');
fs.createReadStream(bigFile).pipe(process.stdout)
```

## 流的基础

stream 提供了以下四种类型的流:

```js
const stream = require('stream')

const Readable = stream.Readable

const Writable = stream.Writable

const Duplex =stream.Duplex

const Transform = stream.Transform
```



### Readable（可读流）

首先我们需要从数据资源中读取数据，并通过push方法将数据传送到可读流中供下游消耗，这就会触发以下事件。

```js
readable.on('data', data => process.stdout.write(data))
```

值得注意的是当读取完毕后必须push（null）来结束流，并且在流结束后并不能在push数据。

上述例子中的process.stdout 代表标准输出流，实际是一个可写流，我们可以通过这种方式消耗数据流，当数据流消耗完后，就会触发end时间。



### Writable（可写流）

与可读流相似，上游通过调用 writable.write(data)将数据写入可写流中,再通过_write方法写入底层，通过调用next方法获取下一个数据，上游需要通过writable.end()方法结束流传递。

```js
const Writable = require('stream').Writable
const writable = Writable()
writable._write = function (data, enc, next) {
	// 将流中的数据写入底层 
	process.stdout.write(data.toString().toUpperCase()) 
  // 写入完成时，调用`next()`方法通知流传入下一个数据 
  process.nextTick(next)
}
// 所有数据均已写入底层 
writable.on('finish', () => process.stdout.write('DONE'))
```

### Duplex（可读可写流）

Duplex 实际上就是继承了 Readable 和 Writable。 所以，一个 Duplex 对象既可当成可读流来使用，也可当成可写流来使用，因为它既可读又可写，所以称它有两端:可写端和可读端。 可写端的接口与Writable 一致，作为下游来使用;可读端的接口与 Readable 一致，作为上游来使用。

### Transform

在Transform中可写端写入的数据经变换后会自动添加到可读端，Tranform继承自 Duplex，并已经实现了读和写的方法，同时要求用户自定义一个转化方法。

```js
const Transform = require('stream').
Transform class Rotate extends Transform {
  constructor(n) {
    super()
// 将字母旋转`n`个位置
    this.offset = (n || 13) % 26
  }
// 将可写端写入的数据变换后添加到可读端
  
	_transform(buf, enc, next) {
		var res = buf.toString().split('').map(c => {
		var code = c.charCodeAt(0)
    if (c >= 'a' && c <= 'z') {
			code += this.offset
			if (code > 'z'.charCodeAt(0)) {
				code -= 26 
   	  }
		} else if (c >= 'A' && c <= 'Z') { 
      code += this.offset
			if (code > 'Z'.charCodeAt(0)) {
				code -= 26 
      }
		}
	return String.fromCharCode(code) }).join('')
// 调用 push 方法将变换后的数据添加到可读端 this.push(res)
// 调用 next 方法准备处理下一个
	next()
	}
}
var transform = new Rotate(3)
transform.on('data', data => process.stdout.write(data))
transform.write('hello, ')
transform.write('world!')
transform.end()
```

