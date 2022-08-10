# DApp-tutorial
### Hardhat 新手上路
分享參考各式教學在以太Rinkeby測試鏈上建立一個自己的Token和DApp

參考資料：
1. [hardhat tutorial](https://hardhat.org/tutorial)
2. [完整的Hardhat實踐教程](https://medium.com/my-blockchain-development-daily-journey/%E5%AE%8C%E6%95%B4%E7%9A%84hardhat%E5%AF%A6%E8%B8%90%E6%95%99%E7%A8%8B-a9b005aa4c12)
3. [PecuLab共學Youtube](https://youtu.be/0rlY6WUtrAY)
4. [PecuLab Github](https://github.com/pecu/PecuLab4SEP)
* 小提醒1：Rinkeby測試鏈2022/10/05就不支援了，建議測試換到Goerli測試鏈。我懶得領測試幣，所以在還有一些餘額的Rinkeby上測試XD
* 小提醒2：Hardhat的[boilerplate repo](https://github.com/NomicFoundation/hardhat-boilerplate)可以直接RUN起一個DApp，但是我想要建立自己的Token，所以沒有用他的repo，懶惰的人可以直接去看boilerplate repo就好了～

龜速更新中.....
預計20220811會把所有流程和檔案上傳

## Steps
### Hardhat前置作業
1. `npm install --save -dev hardhat`
2. `npx hardhat` 
![](figures/hardhat_init.png)
後面會用React來建立DApp，所以這邊選第一個。
3. 這可選擇要不要裝，這是用openzeppelin來產生合約的套件，合約也可以用hardhat提供的範本或自己寫
`npm install @openzeppelin/contracts`
### 建立自己的 Token
1. 利用[openzeppelin](https://docs.openzeppelin.com/contracts/4.x/wizard)建立自己的Token
![](figures/openzepplin.png)
2. openzeppelin都填好了之後可以直接下載[檔案](hardhat/contracts/PokenTest.sol)，放到contract資料夾裡
    * 這邊要注意solidity的版本，在openzeppelin預設的是^0.8.4，要改成跟hardhat.config裡面一樣的"0.8.9"
3. 去[Alchemyapi](https://dashboard.alchemyapi.io/)申請API_URL

    step1. ![](figures/API_step1.png)
    step2. 這邊選Goerli比較好喔![](figures/API_step2.png)
    step3. 這邊點下去可以看到URL和API KEY![](figures/API_step3.png)

4. 建立一個.env檔案，內容如下：私鑰很重要，不要被別人看到了！
```
URL=https://eth-rinkeby.alchemyapi.io/v2/<你的API_KEY>
PRIVATE_KEY= 你的錢包私鑰
```
5. 到[hardhat.config](hardhat/hardhat.config.js)裡設定network和帳戶資訊然後跑下面兩個指令
    * `npm install dotenv`
    * `npm install dotenv --save`
6. 修改[deploy](hardhat/scripts/deploy.js)檔案
7. 修改[test](hardhat/test/Test.js)檔案
8. test完OK就deploy
```
npx hardhat test
npx hardhat run scripts/deploy.js --network rinkeby
```
![](figures/test_success.png)
9. deploy成功會出現token的address
`Poken address: 0x73715Ec8e26FF669F246753699e618871E430f52`
![](figures/deploy_success.png)
10. 複製這個token address就可以加到matamask囉！
![](figures/matamask.png)

* 小提醒：如果合約內容有更改的話，都要再重新compile

### 利用React建立DApp
1. `npx create-react-app <<app name>>`
2. 下面的指令可以用來測試前端有沒有連接成功
```
cd <<app name>>
npm start
```
