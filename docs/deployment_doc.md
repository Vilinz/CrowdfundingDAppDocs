## 部署文档

- 部署环境

  Linux操作系统

  nodejs v10.13.0 建议版本在v10.0.0以上

  Truffle v5.1.14 建议版本在v5.0.0以上

  web3 v0.20.6 建议版本在v0.20.0以上

- 智能合约与前端服务器部署

  - 使用npm安装truffle和web3

    ```
    npm install truffle@5.1.14 --save
    npm install web3@0.20.6 --save
    ```

  - 如果还没有安装依赖，通过npm安装依赖

    ```
    npm install
    ```

  - 配置好配置文件，包括网络和测试网区块链钱包等。

    - 在 https://infura.io/ 上申请账号并新建项目。

      ![](https://github.com/Vilinz/CrowdfundingDAppDocs/raw/master/imgs/6-4-1.jpg)

    - 选择ropsten网络并获取项目id，用于部署项目。

    - 获取浏览器metamask插件钱包的助记词mnemonic。

    ```js
    const HDWalletProvider = require("@truffle/hdwallet-provider")
    const mnemonic = "xxx"
    module.exports = {  
        networks: {    
            development: {      
                host: "localhost",      
                port: 7545,      
                gas: 6721975,      
                network_id: "*" // Match any network id    
            },    
            ropsten: {      
                provider: function() {        
                    return new HDWalletProvider(mnemonic, "https://ropsten.infura.io/v3/xxx")      
                },      
                network_id: 3,      
                networkCheckTimeout: 100000    
            }  
        }
    }
    ```

  - 编译智能合约

    ```
    truffle compile
    ```

  - 部署智能合约

    ```
    truffle migrate --network ropsten
    ```

    ![](https://github.com/Vilinz/CrowdfundingDAppDocs/raw/master/imgs/6-4-2.jpg)

    ![](https://github.com/Vilinz/CrowdfundingDAppDocs/raw/master/imgs/6-4-3.jpg)

    ![](https://github.com/Vilinz/CrowdfundingDAppDocs/raw/master/imgs/6-4-4.jpg)

  - 运行前端服务器

    ```
    npm run start
    ```

- 辅组后端服务器部署

  - 在backend文件夹下运行服务器

    ```
    node main.js
    ```

    