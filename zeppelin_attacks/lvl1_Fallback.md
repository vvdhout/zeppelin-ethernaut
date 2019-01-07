# Level 1 - Fallback

### Goal 
We need to claim ownership (owner = player) and empty the contracts balance. This is also the order in which we need to do this. 

### Approach
First we are going to contribute() a modest amount of 1000 wei which will set our contributions mapping to > 0 (which we need in order to make the fallback function not revert).
After having done this we can now initiate the fallback function which (if the value we send > 0 and our contrbutions mapping > 0) will set the owner variable to our address (that of msg.sender). After this we can withdraw() the entire balance.

```
contract.contribute({value: 1000});
... wait for transaction to be mined ...
contract.sendTransaction({value: 100});
... wait for transaction to be mined ...
contract.withdraw();
``` 