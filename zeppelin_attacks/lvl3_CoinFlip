# Level 3 - Coin Flip

### Goal
We need to gues the correct flip() 10 times in a row to get a consecutiveWins of 10.

### Approach
All variables in the contract are open to the public (even if they are set to private) and variables such a block.timestamp, block.number, and so forth, are manipulable by the miners. What we can do is just recreate this contract to guess the outcome while immediately calling the original flip() function at the end of the function. This way we also use the exact same value for block.number and thus block.hash.

### Resolution
True randomness is practically impossible in Solidity smart contracts given the accessibility of all variable values and the determination of block... values.