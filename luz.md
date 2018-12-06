# Every day of Rust: 2nd

##二.rust的安装&包管理&项目代码目录结构

#### 先说明下Rust的语言版本
nightly (是功能最丰富的,每天都要在github主版本中自动创建的版本 )
beta (每隔一段时间从nightly何必过来一些特性,可以理解成预发布版本)
stable  (正式版本,从beta版本中合并新功能)

#### rust的语言版本管理&项目依赖库
*脚本语言：*
大家如果玩过其他语言，应该知道rust在区块链上的一个对手，Go语在版本切换,包管理方面是很糟糕的. 玩过nodejs知晓,切换nodejs的版本,需要用到nvm.包的管理用npm,yarn. 这种体验是非常爽的。而Python在这方面也在演化,过去用沙盒环境+pip的时代一去不复返.pipenv+pyenv+autoenv安装+环境变量设置可以达到nodejs的nvm+npm的效果.当然python需要安装配置太多。且依赖库的目录在沙盒中，而不在当前项目中，这几种语言在便利程度上，nodejs是最方便的。

*编译语言：*
上面的几个都是较为易用的脚本动态语言，而底层的编译语言如c/c\++则很苦恼
 c/c\++的编译,项目稍微大一点多需要makefile文件。语言版本切换？项目依赖库？恩，历史原因，早期基本没有，后期也没有统一的工具，所以基本上非常麻烦的。

*那么我们的rust呢？*
我们在玩转rust时,在这方面的体验，甚至会超越nodejs.
 rust官网有一个叫rustup的语言环境管理的工具,nodejs的nvm是第三方开发,不强制使用,而rustup则是rust官方出品,安装rust语言本身,实质上就前提就是安装了rustup.当然还送一个cargo。


本文我们将从安装rustup开始，分别讲述rustup，rustc，cargo。你将掌握rust的安装，编译运行，以及语言管理，依赖包管理工具的使用。

## rustup的使用-rust的安装
*install rustup*
Mac 或 linux :
curl https://sh.rustup.rs -sSf | sh 
(Ps:在国内,有时需要代理,原因你懂得..)
安装完成后会送rustup,rustc和cargo

#### rustup使用
Rustup
按照前问所述，安装完成后,可熟悉下rustup的常见命令:
*查看rustup版本:* rustup -V
*安装版本* rustup install   beta| nightly| stable
*切换系统默认的rust版本:* rustup default   beta| nightly| stable
*查看系统已安装的rust版本:* rustup show
*升级rust版本: *rustup update  beta| nightly| stable

#### rustc
Ructc可以编译,运行你的rust代码. 如果只是一个单文件的小脚本,一般用rustc即可.
例如,使用vim编辑一个名为hello.rs的rust源码文件,代码如下,随后执行rustc hello.rs 会在当前目录下生成一个 名为hello的二进制可执行文件,然后我们运行这个二进制文件:

fn main() {
    println!("Hello, world!");
}
(img)
这下你应该体会到，rust不是动态的脚本语言,而是需要编译生产可执行文件的静态语言了吧。 


我们在文章开头有对比几种语言的的依赖库包管理。而你已经知晓，rust不是动态的脚本语言。所以还有一个编译执行上的问题。对的，cargo就是解决这一切的工具：

#### cargo
因为rust本身是编译执行文件，再执行的语言。（非动态语言）。
所以cargo处理管理项目依赖库，还具备编译执行项目的能力。和rustc类似，cargo也是rustup送的。
*1.我们先使用cargo创建一个项目：*
#需注意 不加--bin，则创建的是一个依赖库。而非可执行文件
cargo new hello\_cargo --bin 

生成的项目包含一个Cargo.toml文件和src文件夹。这类似npm init的效果。
(img)
*2.如何编译cargo项目呢？执行cargo build即可。*
(img)
其中target就是目录里是编译通过的二进制可执行文件。
(img)

需要注意，cargo build 和cargo build —release 是不一样的。后则的可执行文件是./target/release/项目名，而前者是./target/debug/项目名

ps：*关于cargo build—release*
当您的项目准备发布时，才使用 cargo build --release 来优化编译项目。这会在 target/release 而不是 target/debug 下生成可执行文件。
Release会让编译后的可执行文件，执行更快，但是编译速度会比debug的慢很多。
所以他们的用途：
+ 一种为了开发，你需要经常快速重新构建；
+ 另一种为了构建给用户最终程序，它们不会经常重新构建，并且希望程序运行得越快越好。
如果你在测试代码的运行时间，请确保运行 cargo build --release 并使用 target/release 下的可执行文件进行测试。

*其他cargo常用命令：*
查看cargo版本：cargo --version
检查代码是否可编译：cargo check
安装某个依赖库：cargo install xx（类似npm 或pip/pipenv ）

*3.你也可以直接运行：*
cargo run
(img)

相信关于rustc直接编译运行和使用cargo的过程你已有一定了解。对于小项目（一个脚本）。rustc就好。而当项目够大的时候cargo的优势就体现出来了。

Rust作为后期之作的编译语言，提供了甚至超越脚本语言才有的包和语言版本管理工具（甚至有的语言至今都没有解决的，比如php）。不如我们实践一下：

#### 实践环节：从0安装parity（以太坊rust客户端）


# webassembly的学习（写作一篇题为webassembly为什么是未来的文章，还未写完...）
#### webassembly史前，js如何演化：
这货出现前，前端的圈子也是很乱很乱，一方面js编程入门简单，但是使用难度大。原型链，对象权限，数据类型的转换，异步，线程协程等相比其他语言都不是太简单的。

而为了简化js，jquery流行了一阵，而后出现一些编译后生成js的，如coffeescript然后coffeescript只是让编写js更简单。js还有项目变大以后的代码可维护性也需要解决，而react vue等也在浏览器里（甚至已经侵犯native app的领地）。然后执行效率上并没有提升(用异步，虚拟dom掩盖本身执行效率低的问题)，也不能让其他语言开发者参与进来。
后来js本身也更新了es6，es7规范，甚至于微软的ts则拥有了更多语法特性。然而最后执行的还是老的js，语法解析，编译的过程需要做类型推断，需要断言。都比较耗时。而且js里没有
没办法处理需要较高性能的图形图像的渲染。（好的图像渲染引擎是c/c++写的）。

mozilla推出了asm.js，能够支持将c/c++的库编译后，供js调用。而且也比js本身在执行速度上变快。然而没有得到其他厂商支持。而google也推出了新语言dart，然而也只是在google一家浏览器中能得到支持。
直到asm.js演化成webassembly。而webassembly得到了主流大厂的广泛支持。

#### 什么是webassembly？
#### 什么是webassembly？
待完成..
#### webassembly为什么快：
待完成..

#### webassembly怎么运行（你怎么使用它）
待完成..




#webassembly为什么是未来？
更多语言的参与：
一直以来能参与webassembly的都只是。


区块链智能合约为什么和webassembly结合



主流浏览器


webassembly
[https://www.ibm.com/developerworks/cn/web/wa-lo-webassembly-status-and-reality/index.html]

相信你已经看到，出了写webassembly有些门槛，使用编译后的wasm和js结合是非常简单事，那么我们可以想象：
react，vue用webassembly重写会怎样？10倍的性能提升，会如何？




Pwa让你的页面像app一般丝滑，webassembly让前端更快。graphql让api请求更爽。web取代原生app时代真的要来了。
