# Level 4 - Telephone

### Goal
Claim owernship of the contract (owner = player).

### Aproach
So we can set the owner of the contract if we can get tx.origin != msg.sender. tx.origin is were the transaction call originated and msg.sender is the last address that is actually calling the function. Many a times, these are the same. However, we can easily manipulate this. If we can create a contract with a function that call changeOwner(_owner) we can call this function with our EOA (e.g. the player account)and submit the player address as the argument. Now, we have a tx.origin which is the EOA's address, and a msg.sender which is our new contract's address. Hence, we pass the if statement and set owner = player.

### Resolution
Clearly evaluate whether using tx.origin is really necessary and what the goal is of the function. Be aware of the difference between msg.sender and tx.origin.