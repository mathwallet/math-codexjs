# math-codexjs

## Run
npm run serve

## Use

#### Login
```
// Blockchain
const node_config = {
  blockchain,   // "codex"
  httpEndpoint: node_url,
  chainId
}
const res = await window.mathExtension.getIdentity({blockchain, chainId});
console.log(res.accounts);
```
#### Transfer
``` javascript

// Math Signature Provider
const signProvider = window.mathExtension.codexSignProvider();
// Node config
const node_config = {
  blockchain,   // "codex"
  httpEndpoint: node_url,
  chainId,
  signProvider  // window.mathExtension.codexSignProvider()
}
// transfer
const token = await Codex({
                          signProvider,
                          blockchain, 
                          httpEndpoint, 
                          chainId
                        }).contract('codex.token');
const res = await token.transfer(from, to, quantity, memo);
console.log(res);

```
## Codex.js
https://github.com/codexnetwork/codex-js

## Test

#### Install MathWallet Browser Extension
https://medishares-cn.oss-cn-hangzhou.aliyuncs.com/extension/mathwalletplus-codex.zip
