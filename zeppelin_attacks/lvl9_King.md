# Level 9 - King

### Goal
The goal here is to become king and not allow anybody else to become king after us.

### Approach
This is a replication of a famous hack on a big Ethereum game: King of Ether. We want to become King and make sure nobody can reclaim kingship after us. We can do this by setting up a contract that first claims kingship by sending a transaction with a value > prize. This way we kick the old king out and become king ourselves. Then, we need to make sure we have a fallback function that reverts or throws such that if another address tries to claim kingship by sending a transaction to the King contract that is higher than the new prize, the moment king.transfer(msg.value) is executed it will call our fallback and throw, never getting to the point that it sets a new king.

### Resolution
Always deal with errors when you are making calls to external contracts and expect them to act malicously. If you can deal with a type of error you can make sure the contract does not break as a result. Also, and this is definitely a good option in any case, you can reorganize the function as such that changes are made to the state BEFORE the external call is made. This way you can be sure all modifications will be executed.