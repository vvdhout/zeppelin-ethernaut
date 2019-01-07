# Level 5 - Token

### Goal 
Get more than 20 tokens in your balance, preferably a whole lot.

### Approach
We are going to hack this contract using integer underflow/overflow vulnerabilities. In solidity, if we have an uint (cannot be negative) and we subtract more than the current value, it wraps around to the top (the maximum value over the uint which in this case is 2^256). We can easily hack this contract by initiating the transfer() function with _to = {any address other than player} and _value < 20 (e.g. 30). 20 - 30 will result in a value of 2^256 - 10, which is a whole lot bigger than 0, and thus we pass the require clause. Then our balance is updated to this ridicilous number and the rest of the function executes.

```
contract.transfer(0x643a2734c902764f76f23048df3009e6ff4c7f11, 30);
```

### Resolution
Use a safeMath library such as that of OpenZeppelin that checks the end values for any mathematic operation. Will make sure overflows and underflows do not happen.