# Security Concerns

The following measures are taken to make smart contracts to be secure against common attack.


- Adopting Withdrawal Pattern

  This prevents the ether recipient address to be a malicious contract and render our contract useless.

- Adopting checks-effects-interaction pattern

  This prevents the re-entrancy problem, and prevent users from double-withdrawing ether from our `LotteryPot` contract.

- Adopting circuit breaks pattern

  If there is any security vulnerabilities discovered, all contracts can be set to `disabled` state to limit the loss.

- Using **SafeMath** library for all arithmetic operation

  [SafeMath library from OpenZeppelin](https://github.com/OpenZeppelin/openzeppelin-solidity) is used to perform all `uint` arithmetic operations, so overflow and underflow operations are handled.

- Random number generation takes into account of `block.difficulty`, `block.number`, and `block.timestamp`

  Our random number generation takes into account of three block attributes so that miners are unlikely to tweak the `block.timestamp` to generate result favorable to them.