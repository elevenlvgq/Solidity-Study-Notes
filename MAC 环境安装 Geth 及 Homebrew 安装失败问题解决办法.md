### 安装 Xcode

```jsx
xcode-select –install
```

### 安装包管理工具

```jsx
/usr/bin/ruby -e "$(curl -fsSL 
https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 安装以太坊

```jsx
brew update
brew tap ethereum/ethereum
brew install ethereum
```

### 测试安装结果

`geth --help`

### 以太默认安装路径

`/usr/local/Cellar/ethereum/版本`(我的版本是1.8.2,所以下面的命令中的路径都是1.8.2,如果你的是其他版本,请替换路径)

### 客户端启动

- 创建 `piccgenesis.json` 文件,内容如下

```jsx
{

 "config": {

    "chainId": 10,

    "homesteadBlock": 0,

    "eip155Block": 0,

    "eip158Block": 0

  },

 "alloc"   : {},

 "coinbase" : "0x0000000000000000000000000000000000000000",

 "difficulty" : "0x1",

 "extraData" : "",

 "gasLimit" : "0xffffffffffffffff",

 "nonce"   : "0x42",

 "mixhash"  : "0x0000000000000000000000000000000000000000000000000000000000000000",

 "parentHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",

 "timestamp" : "0x00"

}
```

- 将 `piccgenesis.json` 文件放入 `/usr/local/Cellar/ethereum/1.8.2/bin` 路径
- 执行初始化命令

```jsx
open /usr/local/Cellar/ethereum/1.8.2/bin/
cd /usr/local/Cellar/ethereum/1.8.2/bin/
mkdir /usr/local/Cellar/ethereum/1.8.2/bin/chain
geth --datadir "/usr/local/Cellar/ethereum/1.8.2/bin/chain" init piccgenesis.json
```

- 启动客户端

```jsx
geth --identity "PICCetherum" --rpc --rpccorsdomain "*" --datadir "/usr/local/Cellar/ethereum/1.8.2/bin/chain" --port 8545 --networkid 95518
```

### 客户端连接

客户端连接有两种方案.

- 命令行连接

`geth attach /usr/local/Cellar/ethereum/1.8.2/bin/chain/geth.ipc`

- 钱包图形界面连接

下载官方图形界面钱包`https://www.ethereum.org/`,安装界面(注意启动方式与应用程序不同,如果 `双击` 启动,将会启动新的线程.连接的并不是你启动的客户端.程序再启动一个客户端),使用命令启动`"/Applications/Ethereum Wallet.app/Contents/MacOS/Ethereum Wallet" --rpc http://127.0.0.1:8545`

### 命令创建用户

`personal.newAccount('test-account-1')` (test-account-1为账户钥匙)

### 命令行挖矿

启动矿机 `miner.start()`

停止矿机    `miner.stop()`

mac os 安装Homebrew失败问题解决

[https://juejin.cn/post/6844904152397512711](https://juejin.cn/post/6844904152397512711)

Geth及mac上安装Geth 参考资料
[https://blog.csdn.net/cs380637384/article/details/80017854](https://blog.csdn.net/cs380637384/article/details/80017854)
