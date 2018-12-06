## A little start
### 11/28/2018

#### WebAssembly
学习hello world

https://medium.freecodecamp.org/get-started-with-webassembly-using-only-14-lines-of-javascript-b37b6aaca1e4
#### Parity Bridge
https://www.parity.io/bridging-the-dapp-scaling-now-with-parity-bridge/ 
https://github.com/paritytech/parity-bridge/tree/snd-user-guide 

据说是pokadot的技术

Home是主网，Foreign是一个poa以太坊（所以转账免费） 
##### Home -> Foreign 
几个validator验证到Home上有存款事件（event），就在另一个链上同意发行（相当于多重签名 
##### Foreign->Home 
几个validator验证到Foreign上去转账事件（event），就在Foreign上确认（因为gas费为0），最后由一个人带着合法的信息去Home上触发转账

#### 15分钟substrate撸链
教程 https://hackmd.io/s/SkP1lLZhX

视频from web3 summit
https://www.youtube.com/watch?v=0IoUZdDi5Is&feature=youtu.be

#### cosmos skd教程
听说substrate很多方面都借鉴了cosmos sdk，于是初步跑了下cosmos sdk最新的教程。感觉很是相似。两者都很模块化，将要成为构建区块链的脚手架。以后做链就和现在做dapp一样。那在未来到底是做一条链呢还是做一个dapp呢：取决于成本？开发人员？

https://github.com/cosmos/sdk-application-tutorial/blob/master/tutorial/README.md

## 12/5/2018
### 撸链教程
https://substrate.readme.io/docs/creating-a-custom-substrate-chain

### 视频
https://www.youtube.com/channel/UCSs5vZi0U7qHLkUjF3QnaWg/videos
https://www.youtube.com/watch?time_continue=64&v=26ucTSSaqog
### 文章
[引介 | 从比特币到 Polkado](https://ethfans.org/posts/consensus-and-finality-in-blockchains?from=groupmessage&isappinstalled=0)

[cosmos polkadot大pk](http://8btc.com/thread-192727-1-1.html)

### 观点
看到substrate视频的时候，就觉得ethereum已经是过去时了 

Parity 的行动已经很明显了，先主动 substrate 化主流的 bitcoin, ethereum, zcash… 以太坊无论有任何发展，也只是 parity 的一个 parachain, parity 一直在跟进，至于没有主动或者被动 substrate 化的，就已经在消失的轨道上了

 以太坊上能做的事情，以后polkadot都可以做，substrate这个可以动态升级runtime，一下把以太坊上的dapp甩出好几条街来