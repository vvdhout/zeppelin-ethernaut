# Level 7 - Force

### Goal
Get the ether balance of the contract > 0.

### Approach
This contract does not have any payable functions and does not accept any value... the traditional way. However, we can force a contract to take value by using a selfdestruct() function in another contract. The selfdestruct() function allows us to destroy the contract and its storage from the blockchain and state. While doing this, we can specify an address that will take the remaining ether of the contract and the receiver cannot block this ether from coming in. So, this is what we do. We set up a contract with some ether, and initiate a selfdestruct({Force Contract Address}).

### Resolution
It is not possible to block ether from coming in to the contract address. So, knowing this we can decide how we want to have our contract operate. If it is really important that our contract's balance stays below a certain number, we could accept value with a fallback function and transfer() ether out of the contract if it surpasses this arbitrary amount. Also, we could choose to keep a balance mapping within the contract and have functionality depend on that instead of the actual ether balance inherit to the contract.