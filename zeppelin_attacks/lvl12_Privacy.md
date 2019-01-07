# Level 12 - Privacy

### Goal
Unlock the contract -> locked = false.

### Approach
In order to unlock() the contract succesfully we need to send in a key that equals bytes16(data[2]). As we can see, the data array has been set and stored using the constructor function. We know that this data should be publicly available to us on the blockchain and that we can query this using 
```
await web3.eth.getStorageAt(address, slot)
```
The main thing to figure out here is where exactly the data array, and specifically data[2] is stored. The EVM uses a storage optimization technique that might feel a bit counter-intuitive. In general, it stores every variable in a slot from 0 to ? based on the order in which they are provided in the contract. However, in cases where variables together take up 32 bytes (one slot size) or less they can be stored together in one slot. This way we might even store multiple variable values in one slot. On top of that, after some research, I found out that constant variables are not stored in any slot at all. So we skip over these. Looking at our contract we see the that slot 0 will occupy the locked boolean (1 byte), the flattening variable (8bits -> 1 byte), the denomination variable (8bits -> 1 byte), and the awkwardness variable (16bits -> 2 byte). All of these fit into the first slot (if we getStorageAt() slot 0 we get '0x00000000000000000000000000000000000000000000000000000053afff0a01' where 01 = false bool, 0a = 10, ff = 255, 53af = 21423). The variable we are looking for exists in an array consisting of bytes32 values. Each array item therefore will take up an entire slot. data[0] will be in slot 1, data[1] in slot 2, and data[2] will be in slot 3.
So we query slot 2 of our contract storage:
```
await web3.eth.getStorageAt(contractAddress,3)
> '0x4b88705762773a2cd663475576a5088916d574462c7c830885c7df86d458c8b7'
```
Now we have data[2]. But we need bytes16(data[2]). This means we need to take the first half (16/32 = 0.5) of the hex value and send this as input which unlocks the contract.
```
contract.unlock('0x4b88705762773a2cd663475576a50889')
```