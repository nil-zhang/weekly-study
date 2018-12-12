# webassembly入门1:来龙去脉

## webassembly史前，js如何演化：
这货出现前，前端的圈子也是很乱很乱，一方面js编程入门简单，但是使用难度大。原型链，对象权限，数据类型的转换，异步，线程协程等相比其他语言都不是太简单的。

为了简化js，jquery流行了一阵，而后出现一些编译后生成js的，如coffeescript
然后coffeescript只是让编写js更简单。
后来js本身也更新了es6，es7规范，微软的ts则拥有了更多语法特性，静态类型检查。
而react vue等也在浏览器里（甚至已经侵犯native app的领地）。然后执行效率上并没有提升(用异步，虚拟dom掩盖本身执行效率低的问题)，也不能让其他语言开发者参与进来，同时缺乏类型。
Node.js虽然性能很好，但只限于服务端。浏览器里的js就是一个慢。

#### 历史原因，js存在如下问题：
1.编译执行速度慢，效率不高。
2.语法入门简单，但进阶对其完全掌握却非常难，不同人写的js代码是不一致的。
3.难以控制不出现bug，出现问题也不容易找出问题。
4.缺乏高效的图像渲染类的库，无非满足网游等领域的需求。
5.虽然有了简化的标准如es6，es7但是当前的浏览器未得到全部支持，而ts也一样。这些标准，以及前面提到的react，vue大多需要经过编译生成浏览器执行的js代码，简化了开发，但是编译过程不可控太高。执行效率比起直接执行js就更低了。


## 什么是webassembly？
WebAssembly 是一种新的字节码格式，他支持WebAssembly开发者使用几乎任何的编程语言开发，然后通过编译器，生产WebAssembly字节码文件（.wasm）
而这个字节码文件可以被js的fetch方法读取，并可以执行WebAssembly程序员开发的方法。出了js中可执行wasm文件。
WebAssembly开发者也可以让wasm文件读取js中的接口。

这里需要记住，底层语言如c++作为原生开发语言，开发玩后，经过一个llvm的编译器生成wasm字节码文件。这个字节码文件能达到接近我们下面提到的原生语言生成的二进制文件的执行速度。同时又具有更好的兼容性。
目前支持如下语言编写webassembly （只要支持llvm可运行的语言都行）
c/c++    rust     Kotlin    ts

#### c/c++ rust go等底层语言为什么不行？
这些语言生成的可执行二进制文件受到不同系统，硬件影响较大，难以一套代码所有平台通用。
在浏览器中支持这些语言像js一样使用，更是不可能做到了。
这里提到c/c++等生成的是二进制执行文件，这就区别与上面的提到的webassembly生成的字节码文件了。（webassembly的字节码文件会有一个更加包容性的虚拟机执行）

#### 为什么不是js？
其实webassembly并非要取代js，虽然也可以做到。但是用js做胶水粘合不同的webassembly生成的执行文件可能更新有效。
webassembly开发出的文件在浏览器中，也能达到接近原生性能的速度运行，比起js速度快至少10倍。
开发者可以通过webassembly的编译器把c/c++，rust以及其他语言开发的库编译成webassembly的可执行文件，达到接近10倍的速度。

#### WebAssembly的可能性
Llvm编译器本身可以扩展，他将原省语言生成的wasm字节码文件。可以扩平台执行，当前的浏览器以大低支持（集成了wasm虚拟机）。而公链的虚拟机也可以采用wasm虚拟机。以太坊2.0的ewasm就是这么做的。



## webassembly怎么用（实践指南）
这个例子是AssemblyScript为原生的开发语言。
大概介绍了wasm的始末，以及编译，js执行的过程：
[https://www.ibm.com/developerworks/cn/web/wa-lo-webassembly-status-and-reality/index.html](https://www.ibm.com/developerworks/cn/web/wa-lo-webassembly-status-and-reality/index.html)

编写webassembly的原生语言中如何调用js的api：
[https://developer.mozilla.org/zh-CN/docs/WebAssembly/Using\_the\_JavaScript\_API](https://developer.mozilla.org/zh-CN/docs/WebAssembly/Using_the_JavaScript_API)

[http://webassembly.org.cn/getting-started/js-api/](http://webassembly.org.cn/getting-started/js-api/)

Js中如何调用webassembly编译后的wasm字节码文件：
[https://developer.mozilla.org/en-US/docs/WebAssembly/Loading\_and\_running](https://developer.mozilla.org/en-US/docs/WebAssembly/Loading_and_running)
（大低是用 fetch调取wasm文件）
后期也支持如下标签直接调用wasm（可以做到完全不依赖js）
```bash
<script type="module">

```



## 主要学习网站&文档：
**中文网：**
[http://webassembly.org.cn](http://webassembly.org.cn)

**上文提到ibm的文档（适合入门）：**
[https://www.ibm.com/developerworks/cn/web/wa-lo-webassembly-status-and-reality/index.html](https://www.ibm.com/developerworks/cn/web/wa-lo-webassembly-status-and-reality/index.html)

**Mdn的文档**
[https://developer.mozilla.org/zh-CN/docs/WebAssembly](https://developer.mozilla.org/zh-CN/docs/WebAssembly)
如下图，包含了各种demo示范：
![](DraggedImage.png)

**rust开发者的wasm：**
[https://rustwasm.github.io/book/](https://rustwasm.github.io/book/)

**kotlin开发者的wasm ：**
（kotlin  native默认使用llvm作为编译器）
[[https://kotlinlang.org/docs/reference/js-overview.html]](https://kotlinlang.org/docs/reference/native-overview.html)

**一个webassembly的论坛**
[https://www.w3ctech.com/category/18](https://www.w3ctech.com/category/18)

pwa让你的页面像app一般丝滑，webassembly让前端更快。graphql让api请求更爽。
![](DraggedImage.tiff)

 