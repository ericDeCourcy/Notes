### Compilation

- For the error `stack too deep when compiling inline assembly`, [turning on the optimizer can help resolve it](https://forum.openzeppelin.com/t/stack-too-deep-when-compiling-inline-assembly/11391/10). In my case so far, enabled with 200 runs is enough to fix the problem. 
	- check [this answer on stack overflow](https://stackoverflow.com/questions/70310087/how-do-i-resolve-this-hardhat-compilererror-stack-too-deep-when-compiling-inli) and add the following snippet to your hardhat config:
	- ```
		settings: {
      	optimizer: {
        		enabled: true,
        		runs: 200,
      		}
      ```
      - No need to worry about `yul`, `yulDetails` or `optimizerSteps` for this most of the time

### For scripts and tests:

- For Error message `xxx.yyy is not a function`, even if that function is declared, may be because there are multiple functions with the same name.
	- For example, `approve(address)` and `approve(address,uint256)` may cause calling either of these via hardhat scripts to say `contractName.approve is not a function` 
	- To get around this, change the way you call it:
		- :x: `contractName.approve(target)`
		- :white_check_mark: `contractName["approve(address)"](target)`
		
- If things are acting silly, ensure that you are using `await` correctly in your scripts
	- use `await` before calling smart contract functions to prevent them from getting out of order. However, this strategy may not be sufficient when deploying to actual blockchains
	
- The hardhat simulated blockchain is quite different from an actual decentralized blockchain. 
	- When running scripts which involve multiple transaction calls, on a _simulated_ network those calls will always be mined _exactly_ when they are broadcast
	- When running scripts involving multiple transaction calls on a _real-life blockchain_, there is no guarantee your transactions will be mined at any time.
		- When calling `await myContract.deposit(100)`, the `await` finishes _once the transaction is broadcast_, not once it is mined. So, you will need to do something clever to prevent your transactions from getting out of order 
			- [ ] What do you do? Pretty sure we can use transaction reciepts
		- When running scripts on a real-life blockchain, you may get an error suggesting the nonce is wrong. I believe this is because if you attempt to send 2 transactions two quickly, hardhat will query the chain to see which nonces have been used for your account and then, not seeing that the first tx consumed a nonce (since the tx is just chillin in the mempool), will generate a second tx with the same nonce.
			- [ ] I need to narrow down WHAT the issue is here. Sorry in advance to my readers
		
- calling `let myCall = await myContract.myNonViewFunction()` will await creating of the calling transaction, NOT the mining of said transaction. This is only for non-view functions.
	- This means you won't see the return value of the call to `myNonViewFunction` within `myCall`
	- To actually see what the return of a non-view function call would be, you can do a _simulated_ or _static_ call. Do this by doing `await myContract.callStatic.myNonViewFunction()`. This will NOT generate a transaction, but instead simulate what the return value of that function would be if a transaction making that call was _mined at that time_. It's important to distinguish the transaction being _mined_ from the transaction being _sent_ in some cases.
- calling `let myCall = await myContract.myViewFunction()` will await the return value of the _view_ function. This is because you aren't generating a transaction for this, but rather querying the blockchain. It doesn't require gas or require a sender. 
- [ ] I'd really love to know how to get the `Duplicate definition of XYZ` message to be silenced

- All calls will come from the default signer unless specified differently
	- When just doing local tests on a simulated blockchain, you can use `const [signer0, signer1, ...] = await ethers.getSigners()` for as many signers as you need. Just add them to the list within the `[ ]` brackets
	- To call a function from a different signer (as in, from a different account), use `.connect`:
		- `await myContract.connect(signer1).myFunction()`
		- This will not persist across calls; you'll need to use `.connect(signer1)` every time you want to use `signer1`. Otherwise it will use the default signer.
		
- Here's the command to fast-forward time in the simulated EVM: 
	- `await network.provider.send("evm_increaseTime", [600]);`
		- This increases the time by 600 seconds, or 10 minutes 
### Proxies

- There's OZ's [upgrades plugin](https://www.npmjs.com/package/@openzeppelin/hardhat-upgrades). 
- There's a script in [this medium post](https://medium.com/coinmonks/how-to-create-an-uups-proxy-66eca257b2f9) which is used for deploying a UUPS proxy. Check it out! There are some slick built-in functions for deploying proxies
	- `const uupsProxyPatternV1 = await upgrades.deployProxy(UupsProxyPatternV1, [], {kind: 'uups', unsafeAllow: ['constructor']});`
### Open questions

[ ] How to correctly use `hre.deployments...` functions

[ ] How to correcty use hardhat tasks/subtasks 
