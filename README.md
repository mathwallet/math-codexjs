# math-codexjs

## Run
npm run serve

## Use
``` javascript

// Math Signature Provider
const signProvider = window.mathExtension.codexSignProvider();
// Blockchain
const blockchain = "codex";
// transfer
const config = {signProvider,blockchain, httpEndpoint, chainId};
let token = await Codex(config).contract('codex.token');
let res = await token.transfer(from, to, quantity, memo);
console.log(res);

```
## Codex.js
https://github.com/codexnetwork/codex-js

## Test

#### Install MathWallet Browser Extension
https://medishares-cn.oss-cn-hangzhou.aliyuncs.com/extension/mathwalletplus-codex.zip
