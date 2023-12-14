# Buyer balance not checked before transaction, while assignment of variables occur.

## Severity

### Low risk

## Description

### In the commitBuy function, the buyer's balance need to be have been checked immidetely after 228. Although, safetransfer may revert the transaction and restore all changes to it's original state, I feel is better to revert when balance isn't sufficient immidetely

## Location of Affected Code

File: [StakedCSX.sol](https://github.com/csx-protocol/csx-contracts/blob/main/contracts/Trade/CSXTrade.sol)

```solidity
if (msg.sender == address(ITRADEFACTORY_CONTRACT.buyAssistoor())) {
    if(_buyerAddress == address(0)) {
        revert ZeroAddress();
    }
    _buyer = _buyerAddress;
} else {
    _buyer = msg.sender;
}

if (_buyer == SELLER_ADDRESS) {
    revert NotSeller();
}

referralCode = _affLink;

buyerCommitTimestamp = block.timestamp;

buyer = _buyer;
buyerTradeUrl = _buyerTradeUrl;
```

### Recommendation:

### Make a balance function on the \_buyer once the status of the real buyer has been confirmed
