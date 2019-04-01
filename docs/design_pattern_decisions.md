# Design Patterns

A few design patterns have been adopted in the smart contract implementation.

### Factory Pattern

Instead of saving all lottery pots in a single smart contract. There is a `LotteryPotFactory` that acts as the mother of all contracts, and creating each lottery pot in a separate smart contract. So each smart contract is independent of each others and no potential data leakage. 

Owner of the `LotteryPotFactory` contract also has the right to disable its created `LotteryPot` contracts.

Ref:

- [Solidty Smart Contracts Design Patterns](https://medium.com/@i6mi6/solidty-smart-contracts-design-patterns-ecfa3b1e9784)

### Circuit Breaker Pattern

Circuit breaker functionality has been implemented in both `LotteryPotFactory` and `LotteryPot` smart contract. If security vulnerability is discovered, these contracts could enter a `disabled` state, and thus loss could be limited.

Ref:

- [Circuit Breakers - Smart Contract Best Practices](https://consensys.github.io/smart-contract-best-practices/software_engineering/#circuit-breakers-pause-contract-functionality)

- [Fail Safe Mode - Solidity doc](https://solidity.readthedocs.io/en/v0.5.4/security-considerations.html?highlight=fail%20safe%20mode#include-a-fail-safe-mode)


### Withdrawal Pattern

Withdrawal pattern is applied in `LotteryPot` contract, at the `winnerWithdraw()` and `participantWithdraw()` methods. Instead of initiating the ether transfer from the contract, we ask the target recipient to initiate the transfer and call these methods.

Ref: 

- [Withdrawal from Contracts - Solidity doc](https://solidity.readthedocs.io/en/v0.5.4/common-patterns.html)

### State Machine Pattern

State machine pattern is implemented to keep track of the `LotteryPot` contract state, transitioning from `open`, to `closed` when the pot closed time is reached, to `stakeWithdrawn` when the stake in the pot is withdrawn by the winner.

Ref:

- [State Machine - Solidity doc](https://solidity.readthedocs.io/en/v0.5.4/common-patterns.html?highlight=check-effect-interaction#state-machine)

### Checks-Effects-Interaction Pattern

When transfering ether to external address, we are not sure if the recipient address is a user address, or a malicious contract address that may in turns call our contract withdrawal function again. So we set our internal state first before ether transfer, so it does not allow re-entrancy security vulnerability.

Ref:

- [Re-Entrancy - Solidity doc](https://solidity.readthedocs.io/en/v0.5.4/security-considerations.html)