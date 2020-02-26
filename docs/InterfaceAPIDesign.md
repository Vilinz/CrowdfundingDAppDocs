# 接口文档

<!-- TOC -->

- [简介](#简介)
- [接口调用实例](#接口调用实例)
  - [改变状态](#改变状态)
  - [不改变状态的call](#不改变状态的call)
  - [进一步封装](#进一步封装)
- [Cowdfunding接口](#Cowdfunding接口)
  - [项目开始](#项目开始)
  - [项目审核不通过](#项目审核不通过)
  - [支助项目](#支助项目)
  - [设置证明材料图片](#设置证明材料图片)
  - [检查当前状态并汇款](#检查当前状态并汇款)
  - [提款](#提款)
  - [检查当前项目状态](#检查当前项目状态)
  - [获取项目所有信息](#获取项目所有信息)
  - [获取项目证明信息](#获取项目证明信息)
  - [获取合约余额](#获取合约余额)
  - [获取已经筹集到的资金](#获取已经筹集到的资金)
  - [获取项目支助者](#获取项目支助者)
- [CowdfundingManager接口](#CowdfundingManager接口)
  - [新建项目](#新建项目)
  - [获取项目地址](#获取项目地址)
  - [查询我参与的项目](#查询我参与的项目)
  - [查询我发布的项目](#查询我发布的项目)
  - [获取管理员地址](#获取管理员地址)
- [donator2Cowdfunding接口](#donator2Cowdfunding接口)
  - [参与项目](#参与项目)
  - [查询我参与的项目](#查询我参与的项目)
  - [新建项目存储](#新建项目存储)
  - [查询我发布的项目](#查询我发布的项目)
- [Utils接口](#Utils接口)
  - [byte转string](#byte转string)
  - [string转byte](#string转byte)

<!-- /TOC -->

### 简介

这是整个应用程序的API接口文档，这里的接口与我们普通的web的接口有些不一样，我们是基于区块链的，这里所说的接口是我们用于访问区块链上智能合约的接口。

------

### 接口调用实例

- ------

  #### 改变状态

  ```js
  instance.donate(2, "name", {from: window.web3.eth.accounts[0]}).then(results => {
      
  }).catch(error0 => {
      console.log(error0)
  })
  ```

- ------

  #### 不改变状态的call

  ```js
  instance.getAllInfo.call(currentTimestamp, {from: window.web3.eth.accounts[0]}).then(results => {
      
  }).catch(error0 => {
      console.log(error0)
  })
  ```

- ------

  #### 进一步封装

  ```js
  getDonators_: function (index) {
      let self = this
  
      return new Promise((resolve, reject) => {
          self.instance.getDonators.call(
              index,
              {from: window.web3.eth.accounts[0]}
          ).then(success => {
              resolve(success)
          }).catch(err => {
              reject(err)
          })
      })
  },
  ```

------

### Cowdfunding接口

- ------

  #### 项目开始

  **描述**

  控制项目状态，使其状态变为开始状态。

  **权限与状态**

  管理员权限，改变状态

  **接口**

  ```js
  begin()
  ```

  **返回值**

  无

- ------

  #### 项目审核不通过

  **描述**

  项目在审核阶段不通过，意味着项目失败。

  **权限与状态**

  管理员权限，改变状态

  **接口**

  ```
  rejectProject()
  ```

  **参数说明**

  无

  **返回值**

  无

- ------

  #### 支助项目

  **描述**

  对项目发起捐款

  **权限与状态**

  改变状态

  **接口**

  ```js
  donate(uint256 currentTimestamp, string memory name)
  ```

  **参数说明**

  | 参数             | 说明             |
  | ---------------- | ---------------- |
  | currentTimestamp | 当前时间戳       |
  | name             | 面板上展示的名字 |

  **返回值**

  无

- ------

  #### 设置证明材料图片

  **描述**

  项目新建成功而且图片已上传后端服务器后用于设置项目的图片信息。

  **权限与状态**

  改变状态

  **接口**

  ```js
  setImageInfo(string memory headImage, string memory img1, string memory img2, string memory img3)
  ```

  **参数说明**

  | 参数      | 说明        |
  | --------- | ----------- |
  | headImage | 封面图片url |
  | img1      | 证明图片1   |
  | img2      | 证明图片2   |
  | img3      | 证明图片3   |

  **返回值**

  无

- ------

  #### 检查当前状态并汇款

  **描述**

  检查项目是否结束并汇款。

  **权限与状态**

  管理员权限，改变状态

  **接口**

  ```
  checkStateAndPay()
  ```

  **参数说明**

  无

  **返回值**

  无

- ------

  #### 提款

  **描述**

  项目发起人提款

  **权限与状态**

  发起人权限，改变状态

  **接口**

  ```
  withdrow()
  ```

  **参数说明**

  无

  **返回值**

  无

- ------

  #### 检查当前项目状态

  **描述**

  检查当前项目的状态

  **权限与状态**

  无

  **接口**

  ```
  checkState(uint currentTimestamp)
  ```

  **参数说明**

  | 参数             | 说明       |
  | ---------------- | ---------- |
  | currentTimestamp | 当前时间戳 |

  **返回值**

  | 描述               | 类型 |
  | ------------------ | ---- |
  | 代表项目状态的数字 | uint |

- ------

  #### 获取项目所有信息

  **描述**

  获取项目信息

  **权限与状态**

  无

  **接口**

  ```
  getAllInfo(uint256 currentTimestamp)
  ```

  **参数说明**

  | 参数             | 说明       |
  | ---------------- | ---------- |
  | currentTimestamp | 当前时间戳 |

  **返回值**

  | 描述          | 类型    |
  | ------------- | ------- |
  | id            | uint256 |
  | targetAmount  | uint256 |
  | endTimestamp  | uint256 |
  | title         | string  |
  | description   | string  |
  | phone         | string  |
  | moreInfo[0]   | string  |
  | s             | uint256 |
  | donatorAmount | uint256 |

- ------

  #### 获取项目证明信息

  **描述**

  获取证明材料url

  **权限与状态**

  无

  **接口**

  ```
  getMoreInfo()
  ```

  **参数说明**

  无

  **返回值**

  | 描述 | 类型   |
  | ---- | ------ |
  | url1 | string |
  | url2 | string |
  | url3 | string |

- ------

  #### 获取合约余额

  **描述**

  获取当前合约余额

  **权限与状态**

  无

  **接口**

  ```
  getBalance()
  ```

  **参数说明**

  无

  **返回值**

  | 描述 | 类型    |
  | ---- | ------- |
  | 余额 | uint256 |

- ------

  #### 获取已经筹集到的资金

  **描述**

  获取合约已经筹集到的资金

  **权限与状态**

  无

  **接口**

  ```
  getAmountCollected()
  ```

  **参数说明**

  无

  **返回值**

  | 描述       | 类型    |
  | ---------- | ------- |
  | 筹集的资金 | uint256 |

- ------

  #### 获取项目支助者

  **描述**

  获取对项目发起帮助的捐助者。

  **权限与状态**

  无

  **接口**

  ```
  getDonators(uint index)
  ```

  **参数说明**

  | 参数  | 说明           |
  | ----- | -------------- |
  | index | 开始获取的下标 |

  **返回值**

  | 描述               | 类型        |
  | ------------------ | ----------- |
  | arrIndex有效个数   | uint        |
  | amount捐赠金额数组 | uint256[20] |
  | name捐赠名字数组   | bytes32[20] |
  | addr捐赠地址数组   | address[20] |

------

### CrowdfundingManager接口

- ------

  #### 新建项目

  **描述**

  新建一个项目

  **权限与状态**

  改变状态

  **接口**

  ```
  createCrowdfunding(string memory _title, string memory _description, uint _targetAmount, uint _endTimestamp, address payable _recipientAddress, string memory _phone)
  ```

  **参数说明**

  | 参数              | 说明                 |
  | ----------------- | -------------------- |
  | _title            | 项目标题             |
  | _description      | 项目描述             |
  | _targetAmount     | 项目筹款金额         |
  | _endTimestamp     | 结束时间戳           |
  | _recipientAddress | 项目结束余额接收地址 |
  | _phone            | 受助人电话           |

  **返回值**

  无

- ------

  #### 获取项目地址

  **描述**

  获取当前所有项目地址

  **权限与状态**

  无

  **接口**

  ```
  getCrowdfundingsAddress()
  ```

  **参数说明**

  无

  **返回值**

  | 描述                    | 类型      |
  | ----------------------- | --------- |
  | crowdfundingAll地址数组 | address[] |

- ------

  #### 查询我参与的项目

  **描述**

  查询我当前参与的项目地址

  **权限与状态**

  无

  **接口**

  ```
  queryMyCrowdfundings(address addr)
  ```

  **参数说明**

  | 参数 | 说明     |
  | ---- | -------- |
  | addr | 我的地址 |

  **返回值**

  | 描述       | 类型      |
  | ---------- | --------- |
  | myFundings | address[] |

- ------

  #### 查询我发布的项目

  **描述**

  查询当前地址发布的项目

  **权限与状态**

  无

  **接口**

  ```
  queryMyPublish(address addr)
  ```

  **参数说明**

  | 参数 | 说明     |
  | ---- | -------- |
  | addr | 我的地址 |

  **返回值**

  | 描述      | 类型      |
  | --------- | --------- |
  | myPublish | address[] |

- ------

  #### 获取管理员地址

  **描述**

  获取合约管理员地址

  **权限与状态**

  无

  **接口**

  ```
  getManagerAddr()
  ```

  **参数说明**

  无

  **返回值**

  | 描述    | 类型    |
  | ------- | ------- |
  | manager | address |

------

### donator2Crowdfundings接口

- ------

  #### 参与项目

  **描述**

  参与项目时维护对应状态

  **权限与状态**

  改变状态

  **接口**

  ```
  joinCrowdfunding(address donator, address crowdfundingAddr)
  ```

  **参数说明**

  | 参数             | 说明       |
  | ---------------- | ---------- |
  | donator          | 捐赠者地址 |
  | crowdfundingAddr | 项目地址   |

  **返回值**

  无

- ------

  #### 查询我参与的项目

  **描述**

  查询我参与项目的地址

  **权限与状态**

  无

  **接口**

  ```
  getCrowdfundings(address donator)
  ```

  **参数说明**

  | 参数    | 说明       |
  | ------- | ---------- |
  | donator | 参与者地址 |

  **返回值**

  | 描述                            | 类型      |
  | ------------------------------- | --------- |
  | joinMapping我参与项目的地址数组 | address[] |

- ------

  #### 新建项目存储

  **描述**

  存储我发布项目的映射关系

  **权限与状态**

  改变状态

  **接口**

  ```
  publishCrowdfunding(address owner, address crowdfundingAddr)
  ```

  **参数说明**

  | 参数             | 说明       |
  | ---------------- | ---------- |
  | owner            | 发布人地址 |
  | crowdfundingAddr | 项目地址   |

  **返回值**

  无

- ------

  #### 查询我发布的项目

  **描述**

  查询我发布的项目

  **权限与状态**

  无

  **接口**

  ```
  getMyPublish(address owner)
  ```

  **参数说明**

  | 参数  | 说明     |
  | ----- | -------- |
  | owner | 我的地址 |

  **返回值**

  | 描述                               | 类型      |
  | ---------------------------------- | --------- |
  | publishMapping我发布项目的地址数组 | address[] |

------

### Utils接口

- ------

  #### byte转string

  **描述**

  byte转string

  **权限与状态**

  无

  **接口**

  ```
  byte32ToString(bytes32 b)
  ```

  **参数说明**

  | 参数 | 说明                |
  | ---- | ------------------- |
  | b    | 要转换的bytes32类型 |

  **返回值**

  | 描述        | 类型      |
  | ----------- | --------- |
  | bytes32长度 | address[] |
  | names       | string    |

- ------

  #### string转byte

  **描述**

  string转byte

  **权限与状态**

  无

  **接口**

  ```
  stringToBytes32(string memory source)
  ```

  **参数说明**

  | 参数   | 说明               |
  | ------ | ------------------ |
  | source | 要转换的string类型 |

  **返回值**

  | 描述           | 类型    |
  | -------------- | ------- |
  | result转换结果 | bytes32 |