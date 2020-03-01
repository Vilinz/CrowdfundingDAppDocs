# 智能合约测试

### 测试框架

truffle架构有着其自动化的测试架构来简单地测试智能合约，测试架构提供两种方式来测试合约，分别是

- 用Javascript写测试用例，这种方式就像外部应用执行合约代码一样。
- 用Solidity写测试用例，这种方式就像裸机测试合约一样。

我们这里采用JavaScript来写测试用例。

### 用JavaScript写测试用例

 Truffle使用Mocha测试框架和断言库Chai进行测试，为您提供了一个可靠的框架，可以从这个框架编写JavaScript测试。 

 Mocha是一个功能丰富的JavaScript测试框架，运行在Node.js和浏览器上，使异步测试变得简单和有趣。Mocha测试连续运行，允许灵活和准确的报告，同时将未捕获的异常映射到正确的测试用例 。

但Mocha测试失败一般通过throw异常来处理，非常的繁琐，所以我们采用了一个更加简单常用的断言库chai来处理异常抛出。

### 测试过程

- 安装区块链测试端

  ```
  npm install ganache-cli
  ```

- 编写测试样例

  在test/truffle中编写好每个合约的测试。

- 运行测试

  ```
  npm run test/truffle
  ```


- 测试结果

  ![](https://github.com/Vilinz/CrowdfundingDAppDocs/raw/master/imgs/7-1-1.jpg)