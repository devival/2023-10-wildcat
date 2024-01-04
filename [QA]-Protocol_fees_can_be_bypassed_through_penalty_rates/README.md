# Original link
https://github.com/code-423n4/2023-10-wildcat-findings/issues/597
# Lines of code

https://github.com/code-423n4/2023-10-wildcat/blob/c5df665f0bc2ca5df6f06938d66494b11e7bdada/src/libraries/FeeMath.sol#L45


# Vulnerability details

## Impact
As mentioned in the [previous audit by aleph_v](https://hackmd.io/@geistermeister/r15gj_y1p#Issue-Log), protocol fees can be bypassed while still paying the same rate to the lenders. The issue was neither resolved nor acknowledged.

## Proof of Concept
The overall interest paid by the borrower is the interest times the protocol fee plus any delinquency fees. By setting the delinquency fee percent to the intended interest and then setting the protocol interest percent to zero (or close to zero) the borrower can construct a vault which pays the lenders the same amount of interest via delinquency fees as it would pay via interest. The borrower can increase the liquidity requirements to force payment of persistent delinquency fees. In this case the lenders have no incentive to withdraw as they get the same rate and borrowers pay a net lower fee as no protocol fee is collected. [aleph_v](https://hackmd.io/@geistermeister/r15gj_y1p#Issue-Log), [FeeMath.sol#L45](https://github.com/code-423n4/2023-10-wildcat/blob/c5df665f0bc2ca5df6f06938d66494b11e7bdada/src/libraries/FeeMath.sol#L45)

## Tools Used
Manual Review

## Recommended Mitigation Steps
Charge protocol fees on the extra interest which is paid by delinquent loans.



## Assessed type

Other