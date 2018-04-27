---
title: IOTA
date: 2018-04-27 17:30:50
tags: [exchange,study]
---


[IOTA][1]并不是链，是一个有向不闭环图（Directed Acyclic Graph），Tangle外观像一条围巾，其确认过程就像是织围巾的过程.
![DAG][2]

总供应量为**（3 ^ 33-1）/ 2** 或2,779,530,283,277,761个。所有Token在初始块创建，总数不便，也不用开采.计量符号：**i,Ki,Mi,Gi,Ti,Pi** 1000进制。

有[中文社区][3]和完整的[开发者文档][4]，和对应的[主链浏览器][5] 于[测试链浏览器][6]。提供常用语言的[SDK][7]。

## 共识

IOTA不能开采不需要矿工那如何确认交易？答案就在上图，要发起一笔新交易需要确认之前两笔交易，接口可以获得两个交易用于用于确认。本次交易也需要后续交易确认。未被确认的交易叫做`Tip`。

系统会定时（2分钟）发起一个`0-value transaction` 称之为 MileStone.
所有节点有一个共识：被milestone确认过的交易不在变化。类似于6次确认的概念。 这也解决了不活跃时交易的确认问题。


## 概念与关联

### Seed 
一切源于Seed,Seeds 是一个长度为81的tryes ('9,A-Z')字符串。生成方式：

```sh 
#Linux 
`cat /dev/urandom |tr -dc A-Z9|head -c${1:-81}`
#Mac 
`cat /dev/urandom |LC_ALL=C tr -dc 'A-Z9' | fold -w 81 | head -n 1`
```
Seed加index生成private key 进而生成address，加密算法原因，iota中一个地址只能支付一次，重复使用有被破解的风险。所以每次index使用后自增保证不重复。Seed就相当于私钥，不同的是私钥一般对应一个地址，而Seed与不同的Index组合可以生成多个地址。

> NEVER REUSE ADDRESSES
Because IOTA uses Winternitz one-time signatures, you should never reuse an address after you have spent from it. Continuously reusing private keys gives a sophisticated attacker the ability to forge the signatures, thus being able to steal funds from the respective address.

这里是Seed，私钥和 账号的[官网][8]描述。还有[其他概念][9]的详细描述。

### Transaction
Transaction和其他区块链概念一直，描述一笔或多笔账务明细；包含目标地址和交易量，除此之外还有额外Message和Tag，这里是[详细参数][10]描述。 如何[发起一笔交易][11]。

Transaction的集合称之为`bundle`，相当于block。

## 部署

### 钱包
[钱包下载][12]地址，下载对应版本按提示安装即可。

### IRI

[IRI下载地址][13]。 网上的[安装指南][14]，网上[指南2][15]。安装步骤如下：

1. Install iri Mainnet

    ``` 
    git clone https://github.com/iotaledger/iri.git
    mvn clean package -DskipTests
    java -jar target/iri-1.4.2.3.jar --testnet -p 14265
    ```
2. Install iri Testnet

    ``` 
    git clone https://github.com/iotaledger/iri.git
    #checkout to testnet branch
    git checkout v1.4.2.3-testnet
    mvn clean package -DskipTests
    java -jar target/iri-1.4.2.3.jar --testnet -p 14265
    ```
    默认连接公共测试链，如果要搭建一个私有测试链需要一个[辅助工具][16]用来初始化创世块和设置里程碑。工具安装：
    ``` 
    git clone https://github.com/schierlm/private-iota-testnet.git
    #设置里程碑
    java -jar target/iota-testnet-tools-0.1-SNAPSHOT-jar-with-dependencies.jar Coordinator localhost 14265
    ```
    文档中描述修的改代码是之前版本，4.2.3已不在需要可以忽略。

3. 使用配置文件启动

    ```
    [IRI]
    PORT = 14265
    UDP_RECEIVER_PORT = 14600
    TCP_RECEIVER_PORT = 14700
    NEIGHBORS = udp://p101.testnet.iota.cafe:14666 udp://p102.testnet.iota.cafe:14666
    IXI_DIR = ixi
    HEADLESS = true
    DEBUG = true
    DB_PATH = testnetdb
    ```
     
4. neighbors
TCP:
tcp://p101.testnet.iota.cafe:15666 tcp://p102.testnet.iota.cafe:15666  tcp://p103.testnet.iota.cafe:15666  tcp://p104.testnet.iota.cafe:15666
UDP:
udp://p101.testnet.iota.cafe:14666 udp://p102.testnet.iota.cafe:14666 udp://p103.testnet.iota.cafe:14666 udp://p104.testnet.iota.cafe:14666


        
## Validate 

 https://github.com/domschiener/nostalgia. open html with chrome.

```
curl http://localhost:14265 \
  -X POST \
  -H 'Content-Type: application/json' \
  -H 'X-IOTA-API-Version: 1' \
  -d '{"command": "getBalances", "addresses": ["IMVDY9KSOPVR9SVMOSNMLHBFICBJHJSIGWZWOFNNALPFDPAGGSBJQOUJKDZQHDXYNIKHFDTOOBWCKHQVC"], "threshold": 100}'
```


  [1]: https://iota.org
  [2]: https://files.readme.io/5aa136c-tangle.png
  [3]: http://www.iotachina.com/
  [4]: https://iota.readme.io/
  [5]: https://thetangle.org/transaction/
  [6]: https://testnet.thetangle.org
  [7]: https://iota.readme.io/docs/overview
  [8]: https://iota.readme.io/docs/seeds-private-keys-and-accounts
  [9]: https://iota.readme.io/docs/glossary
  [10]: https://dev.iota.org/introduction/iota-token/anatomy-of-a-transaction
  [11]: https://dev.iota.org/introduction/iota-token/making-a-transaction
  [12]: https://github.com/iotaledger/wallet/releases
  [13]: https://github.com/iotaledger/iri/releases
  [14]: https://forum.helloiota.com/1191/Setting-Up-a-Full-Node-A-Comprehensive-Guide
  [15]: https://medium.com/@scott.tudd/an-almost-complete-guide-to-setting-up-a-full-iota-node-d9784dfdc80
  [16]: https://github.com/schierlm/private-iota-testnet