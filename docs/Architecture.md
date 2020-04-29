# 架构设计、详细设计（BCE方法）到应用程序框架映射指南

### 逻辑架构

逻辑架构由三层模型（表示层，业务层和持久化层）构成。

![](https://github.com/Vilinz/CrowdfundingDAppDocs/raw/master/imgs/5-5-1.jpg)

- 表示层

  在表示层中采用弱化了的MVC架构，在这层提供了用户页面的范围和前端逻辑的实现。

- 业务层

  是表示层与持久化层访问的桥梁，在本项目中的表现是智能合约的业务逻辑实现。

- 持久化层

  对于传统的应用来说持久化层对应与数据库存储，但对于我们这个去中心化应用来说，数据存储是在整个区块链网络中实现的，所以数据的持久化是借助区块链中智能合约的数据存储功能实现的。

------

### 架构目录设计

- 前端 + 智能合约

  ```
  .                                   
  ├── build   
  	└── contracts      
  ├── config 
  	├── eslint 
  	├── postcss
  	├── vue-loader
  	└── webpack
  ├── contracts    
  	├── Crowdfunding.sol
  	├── CrowdfundManager.sol
  	├── Donator2Crowdfundings.sol
  	├── Migrations.sol
  	├── Test.sol
  	├── Utils.sol
  	└── Users.sol
  ├── docs                      
  ├── migrations
  	├── 1_initial_migration.js
  	└── 2_deploy_migrationjs
  ├── node_modules
  ├── scripts                     
  ├── src
  	├── assets
  	├── components
  		├── DetailPage.vue
  		├── HomePage.vue
  		├── ManagerPage.vue
  		├── MyPage.vue
  		├── MyPublish.vue
  		├── ProjectPage.vue
  		├── PublishPage.vue
  		└── Verify.vue
  	├── js
  		├── Crowdfunding.js
  		├── CrowdfundingInstance.js
  		├── CrowdfundingManager.js
  		├── Users.js
  		└── Utils.js
  	├── router
  		└── index.js
  	├── theme
  		└── element
  	├── App.vue
  	├── main.js
  	└── store.js
  ├── static
  ├── test
  	├── e2e
  	├── truffle
  	└── uint
  ├── index.html
  ├── LICENSE
  ├── package.json
  ├── README.md
  └── truffle-config.js
  ```

- 后端

  ```
  .
  ├── node_modules
  ├── upload
  ├── package-lock.json
  └── main.js
  ```

------

### ECB

- Boundary对象

   表示参与者与系统之间进行的交互以及信息交流 。

- Controller对象

   一个用例具有的事件流的控制行为 。 处理外部事件，实现控制流的类。通常是一个子系统、一个用例一个类 。

- Entity对象

   领域对象或数据实体 。

------

### 映射指南

 项目框架基本上是经典的三层架构，前端UI和业务逻辑是Vue.js，后端接受请求并返回数据是区块链平台，数据库是区块链中智能合约所持有的存储空间。逻辑图对应目录结构是UI层（Vue.js）对应目录src（前端），中间Domain层主要对应目录contract。最后，整个区块链网络是我们的分布式数据库，非常典型的三层架构。ECB的对应则是Boundary对应UI层（前端），Controller对应Domain（智能合约），Entity对应Technical Services（区块链中存储空间）。

除此以外，我们的辅助后端也是属于Domain层，其中文件夹是存储空间，由于文件名对应关系存储在区块链的智能合约当中，所以数据库部分也在区块链当中。 