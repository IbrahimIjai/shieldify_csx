# Creating a New trade contract

## Severity

### Low risk

## Description

### The current storage of contract in the contractAddressToIndex isn't comprehensive enough, there might be issues with debugging and easy comprehension

## Location of Affected Code

File: [StakedCSX.sol](https://github.com/csx-protocol/csx-contracts/blob/main/contracts/TradeFactory/CSXTradeFactory.sol)

```solidity

bool nS = tradeFactoryBaseStorage.newTradeContract(
    params.itemMarketName,
    params.tradeUrl,
    params.assetId,
    params.inspectLink,
    params.itemImageUrl,
    params.weiPrice,
    params.skinInfo
);

if (!nS) {
    revert NoTradeCreated();
}

uint256 _tContracts = tradeFactoryBaseStorage.totalContracts();
address newAddress = tradeFactoryBaseStorage
    .getLastTradeContractAddress();

isTradeContract[newAddress] = true;

contractAddressToIndex[newAddress] = _tContracts - 1;


```

## Recommendation

## newTradeContract can be made to return an contract address and the actual contract index/count to ensure easy debugging and comprehension, and consistensy. This will make easy storage of newaddress and it's count in the contractAddressToIndex mapping in one go.

## Team Response
