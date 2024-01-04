# Original link
https://github.com/code-423n4/2023-10-wildcat-findings/issues/606
# Lines of code

https://github.com/code-423n4/2023-10-wildcat/blob/c5df665f0bc2ca5df6f06938d66494b11e7bdada/src/market/WildcatMarket.sol#L86


# Vulnerability details

## Impact
According to the docs, the lender that deposits 133.7 XYZ tokens into a market will receive 133.7 market tokens - with the market token name depending on what was selected by the borrower when the market was launched.

However, the above architecture does not handle the case when XYZ is a rebasing (or elastic) token whose supply is algorithmically adjusted. The issue might lead to a permanent loss of funds as tokens would stay locked in the contract.

The issue also breaks the following property: `The supply of the market token and assets owed by the borrower should always match.`

## Proof of Concept
[Wildcat-Gitbook#deposits](https://wildcat-protocol.gitbook.io/wildcat/using-wildcat/day-to-day-usage/lenders#deposits)
[WildcatMarket.sol#L86](https://github.com/code-423n4/2023-10-wildcat/blob/c5df665f0bc2ca5df6f06938d66494b11e7bdada/src/market/WildcatMarket.sol#L86)

## Tools Used
Manual Review

## Recommended Mitigation Steps
1. You can explicitly state in the documentation that you do not support rebasing mechanism. 
2. Alternatively, when rebasing tokens go down in value, you should have a method to update the market tokens' balances accordingly. 
And when they go up in value, you should add a method to actually transfer the excess tokens out of the protocol. This is a complex solution.


## Assessed type

ERC20