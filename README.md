# API Documentation

## Examples
Node.js example of how to connect to the post API (requires request) https://pastebin.com/kskMYyzU

## Public API Methods
There are two public methods, all of which take HTTP GET requests and return output in JSON format:

### getBuySellRequests
Returns the buy and sell requests for a coin.

Call: https://gneiss.io/api/getBuySellRequests?address= [address of coin]

### getHistoryRequests
Returns the history requests for a coin:

Call: https://gneiss.io/api/getHistoryRequests?address= [address of coin]

## Trading API Methods
To use the trading API, you will need to create an API key.

All calls to the trading API are sent via HTTP POST and must contain the following headers:

key - Your API key.
sign - The query's POST data signed by your key's "secret" according to the HMAC-SHA512 method.
Additionally, all queries must include a "nonce" POST parameter. The nonce parameter is an integer which must always be greater than the previous nonce used.

Other POST parameters are indicated for each method below with quotation marks

There are several methods accepted by the trading API:

### exchangeInfo
Returns name of your exchange and all of your balances. Sample output:

{
  "btcInfo": {
    "balance": 0,
    "btcInExchange": 0
  },
  "exchangeAddress": "0x...",
  "exchangeInfo": {
    "balance": 0
  },
  "exchangeName": "My Exchange",
  "tokens": [
    "..."
  ],
  "totalValueOfExchange": 0,
  "totalValueOfExchangeETH": 0
}
Call: https://gneiss.io/api/exchangeInfo

### getMyBuySellRequests
Returns your buy and sell requests for a coin. Also contains if the user is the owner of the coin and if the coin is mintable/burnable. Requires the "address" as a POST parameter. Sample output:

{[buy: [...], sell: [...], isOwner: true, canMintBurn: true]}
Call: https://gneiss.io/api/getMyBuySellRequests

### cancelBuyRequest
Cancels a buy request. Requires "id" of the buy request as a POST parameter. Sample output:

Buy Request Removed

Call: https://gneiss.io/api/cancelBuyRequest

### cancelSellRequest
Cancels a sell request. Requires "id" of the sell request as a POST parameter. Sample output:

Sell Request Removed

Call: https://gneiss.io/api/cancelSellRequest

### sendCoin
Send a coin. Requires "to" address to send to, "amt" for amount of coin to send, and "address" of coin to send. Returns Hash of transaction. Sample output:

0x...

Call: https://gneiss.io/api/sendCoin

### sellCoin
Sell a coin. Requires "price" to sell at, "amt" for amount of coin to sell, and "address" of coin to sell. Sample output:

Sell Request Created

or

Sell Completed

Call: https://gneiss.io/api/sellCoin

### buyCoin
Buy a coin. Requires "price" to buy at, "amt" for amount of coin to buy, and "address" of coin to buy. Sample output:

Buy Request Created

or

Buy Completed

Call: https://gneiss.io/api/buyCoin

### mintCoin
Mint a coin. Must be owner of coin and coin must be mintable. Requires "amt" for amount of coin to mint, and "address" of coin to mint. Sample output:

Hash: 0x...

Call: https://gneiss.io/api/mintCoin

### burnCoin
Burn a coin. Must be owner of coin and coin must be burnable. Requires "amt" for amount of coin to burn, and "address" of coin to burn. Sample output:

Hash: 0x...

Call: https://gneiss.io/api/burnCoin

### removeCoin
Removes a coin from your exachange. Requires "hash" of coin Sample output:

Coin Removed

Call: https://gneiss.io/api/removeCoin
