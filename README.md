# UniversalNFTMarketplace
Universal NFT Marketplace

## Key features

 ### ERC721Enumerable as a nft standard
 We use open-zeppeline erc721Enumerable as a standard for base NFT token
 This standard means that every created token are stored and can be operable from one singleton-like contract as **record**
 Instead of creating new instance of contract each time someone create new token
 This help us to save the gas and reduce universe entropy!
 
 For more info see `./contracts/721/singleton/MSNFT.sol `

 ### Currencies erc20
 We use some stable-coins and other erc20 tokens as currencies
 So users can set up and get paid in USDT,USDC,DAI, MST or other custom currencies

 For more info see `./contracts/721/singleton/CurrenciesERC20.sol`


 ### Tokensale721 for initial crowdsale

 User can start/plug crowdsale for any emitted tokens
 We consider this crowdsale to be the *initial* form of sale

 We also consider, that there should be exchange for secondary market
 (P2P exchange of any NFT's from anywhere else platform)
 Exchange will come to v0.2 (not in first version)

 TokenSale contract is a modified OZ crowdsale contract
 It has been modified to work with ERC721 token and get ERC20 tokens as payment

 ### MetaMarketplace
 Any previously minted NFT may be listed for purchase on secondary market
 Each created marketplace is a struct tethered to nft-token contract

 Users may set price in ERC20 tokens, make & receive buy offers
 Whenever users see tokens they want to purchase, they may create and send a buy offer
 Seller may accept the offer or decline it, which will (or will not, basing on seller's decision) trigger the funds (and, of course, token itself) transfer mechanism

 For more info see `./contracts/721/singleton/MetaMarketplace.sol`

 ### MasterCopy and Items
Each token represent some file, so it stores link to the file and some meta-information about NFT as MasterCopy
Any tokens are considered items and attached to specific master-copy, which contain meta-info about NFT
Tokens do not store this info but it can be obtained by links

**So each item (token) is a link to specific master-copy which contain link to the file**




 ## Install

 This is a truffle project, so fist you need to get truffle by
 ` npm install -g truffle `

Download project dependencies:
`npm i`

 Deploy into blockchain / ganache :
 ` truffle migrate --reset `
 (reset flag will do clean migration)

 Deployment scheme can be found in `./migrations/2_deploy_contracts.js`

 Networks configs `./truffle-config.js`

 If you want to test contract locally you may also need ganache
 Contracts ABI (build artifacts) would be found in ./build directory after any sucessfull migration

## Testing
Tests are in directory `./test`

To run tests run ` truffle test `

### Debuging
By default truffle will run tests in test enviroment, described as `development` network in truffle-config.js
Make sure you have ganache up and running, cause `development` end-point are looking for ganache

**What should I do when test fails?**
If tests fail with any revert message you should use truffle debugger, to understand at which point execution fails <br />  
There are different ways to approach debugger, let's see how we can use it

#### A. Make `debug()` wrapper at failed strings at test as described here:
https://www.trufflesuite.com/docs/truffle/getting-started/debugging-your-contracts <br />  
After you have wrapped failed test invokation in test.js, run ` truffle test --debug` <br />  
**Sometimes this method does not work as intended**, so in this case you may try to <br />  
` truffle test --debug -b` or `truffle test ./test/test.js --debug -b` or even ` truffle test --debug --stacktrace -b ` <br />  
If none of it work's try method B <br />  

#### B. Make manual debugging of failed tx:
1. at ganache switch to tab `logs`, make clear logs
2. run ` truffle test -b `
3. find in logs last transaction, which fail, copy it's txid
4. run `truffle debug <failed_tx_id> ` -- it will start truffle in CLI debug mode, where you can expect execution of tx line by line
5. find at which line exactly tx have been failed and why (try to use breakpoints, watch variables, arguments and so on)
6. report problem


 ## Contracts description
