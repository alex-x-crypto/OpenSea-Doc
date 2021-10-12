# OpenSea-Doc
OpenSea Doc

## 1. WyvernProxyRegistry

<https://etherscan.io/address/0xa5409ec958c83c3f309868babaca7c86dcb077c1#code>

## 2. WyvernExchange

<https://etherscan.io/address/0x7be8076f4ea4a4ad08075c2508e481d6c946d12b?__cf_chl_captcha_tk__=pmd_Aths8T0iLFywXibstzXmDNvGlskWKx1AblKvWuYqar8-1633676860-0-gqNtZGzNA1CjcnBszQrR#code>


## 用户流程

1. 注册代理 Register Proxy (调用`WyvernProxyRegistry.registerProxy()`);
2. 买卖（由购买方发起交易）
```
WyvernExchange.atomicMatch_(
    address[14] addrs, 
    uint256[18] uints, 
    uint8[8] feeMethodsSidesKindsHowToCalls, 
    bytes calldataBuy, 
    bytes calldataSell, 
    bytes replacementPatternBuy, 
    bytes replacementPatternSell, 
    bytes staticExtradataBuy, 
    bytes staticExtradataSell, 
    uint8[2] vs, 
    bytes32[5] rssMetadata
)
```

### `atomicMatch_`函数参数含义

-  `address[14] addrs`
-  `uint256[18] uints`
-  `uint8[8] feeMethodsSidesKindsHowToCalls`
-  `bytes calldataBuy`
-  `bytes calldataSell`
-  `bytes replacementPatternBuy`
-  `bytes replacementPatternSell`
-  `bytes staticExtradataBuy`
-  `bytes staticExtradataSell`
-  `uint8[2] vs`
-  `bytes32[5] rssMetadata`

`Order`数据结构
```javascript
/* An order on the exchange. */
struct Order {
    /* Exchange address, intended as a versioning mechanism. */
    address exchange;
    /* Order maker address. */
    address maker;
    /* Order taker address, if specified. */
    address taker;
    /* Maker relayer fee of the order, unused for taker order. */
    uint256 makerRelayerFee;
    /* Taker relayer fee of the order, or maximum taker fee for a taker order. */
    uint256 takerRelayerFee;
    /* Maker protocol fee of the order, unused for taker order. */
    uint256 makerProtocolFee;
    /* Taker protocol fee of the order, or maximum taker fee for a taker order. */
    uint256 takerProtocolFee;
    /* Order fee recipient or zero address for taker order. */
    address feeRecipient;
    /* Fee method (protocol token or split fee). */
    FeeMethod feeMethod;
    /* Side (buy/sell). */
    SaleKindInterface.Side side;
    /* Kind of sale. */
    SaleKindInterface.SaleKind saleKind;
    /* Target. */
    address target;
    /* HowToCall. */
    AuthenticatedProxy.HowToCall howToCall;
    /* Calldata. */
    bytes calldata;
    /* Calldata replacement pattern, or an empty byte array for no replacement. */
    bytes replacementPattern;
    /* Static call target, zero-address for no static call. */
    address staticTarget;
    /* Static call extra data. */
    bytes staticExtradata;
    /* Token used to pay for the order, or the zero-address as a sentinel value for Ether. */
    address paymentToken;
    /* Base price of the order (in paymentTokens). */
    uint256 basePrice;
    /* Auction extra parameter - minimum bid increment for English auctions, starting/ending price difference. */
    uint256 extra;
    /* Listing timestamp. */
    uint256 listingTime;
    /* Expiration timestamp - 0 for no expiry. */
    uint256 expirationTime;
    /* Order salt, used to prevent duplicate hashes. */
    uint256 salt;
}
```

NFT示例程序

<https://github.com/ProjectOpenSea/opensea-creatures>