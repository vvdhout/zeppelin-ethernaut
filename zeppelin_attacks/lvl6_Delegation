# Level 6 - Delegation

### Goal
Claim ownership of the contract (owner = player).

### Approach 
Using delegate.call is always tricky because it allows the called contract to operate from within your context (e.g. when they call another contract, msg.sender will be your address). Having another contract run in your context with delegatecall also means that there value storage will be your value storage. In other words, if that contract normally would store a value at slot 0 when running a function, it will now store it at your contracts slot 0.
So, knowing this, if we can have the Delegation contract call the Delegate contract's pwn() function so that it will store a value to our own owner variable (slot 0). If we call the fallback function (by sending a transaction with msg.data that does not match a method call of our own contract) with our player address as sender and bytes4(keccak256('pwn()')) as the msg.data, we can perform a delegatecall to the Delegate's contract and execute the pwn() method.

```
await web3.eth.sendTransaction({from: player, to: contract.address, data: '0xdd365b8b0000000000000000000000000000000000000000000000000000000000000000'}, (error,result) => {console.log(error + result);});
```

### Resolution
Be very, very carefull when using delegatecall(). You have to know 100% how the contract/libary you are calling handles your call and you need to be constantly aware of potential changes to the library (they can have a certain upgradability).
