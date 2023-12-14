# Net value calculation

## Severity

### Low

## Description

### There has been usage of an integer, 50, which is hard coded in the if statement. this value looks like it is likely to change base on changes in business terms. It should not be hard coded. Secondly, safemate library should be employed to avoid unforseen overflow or underflow issues.

## Location of Affected Code

### line 64, 74

File: [StakedCSX.sol](https://github.com/csx-protocol/csx-contracts/blob/main/contracts/Referrals/NetValueCalculator.sol)

```solidity

if (discountRatio > 50) {
     revert InvalidDiscountRatio(discountRatio, 50);
 }

 if (isBuyerAffiliated) {
    discountedFee = (fullItemPrice * baseFeePercentTen * discountRatio) / 100000; // divide by 100000 instead of 10000
    affiliatorNetReward = (fullItemPrice * baseFeePercentTen * (50 - discountRatio)) / 100000; // divide by 100000 instead of 10000
} else {
    discountedFee = 0;
    affiliatorNetReward = 0;
}
```

#### Recommendation:

#### Use a variable and a function to update the variable for the Use of SafeMath to make the calculations more safer. there might be over flow issues when extreme values are used. it may be left as it is, but might be fine, but it is always safer to use savemath for such.

## Team Response
