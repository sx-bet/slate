# Orders

## Get active orders

```shell
curl --location --request GET 'https://api.sx.bet/orders'
```

> The above command returns JSON structured like this

```json
{
  "status": "success",
  "data": [
    {
      "fillAmount": "0",
      "orderHash": "0xb46e5fff6498f061e93c4f5ed501ee72d924180d6aa78cdfd4d188d3383c91d4",
      "marketHash": "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
      "maker": "0x63a4491dC73245E181c47BAe0ae9d6627E56dE55",
      "totalBetSize": "10000000000000000000",
      "percentageOdds": "70455284072443640000",
      "expiry": 2209006800,
      "apiExpiry": 1631233201
      "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
      "executor": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
      "salt": "69415402816762328320330277846098411244657139277332120954321492419616371539163",
      "isMakerBettingOutcomeOne": true,
      "signature": "0x2aaea5b7c86166c0fbf2745c66aff794a23d21ac71ee143d08706700adbb59aa4c9b862286cf736acae5a74b10847ced73b628f4396eaab0af13b0c637fe4d021b",
      "createdAt": "2021-06-04T17:42:07.257Z"
    },
    {
      "fillAmount": "0",
      "orderHash": "0xd055d177477bd19faa9bad5cb4f907d8ebe069b614bb708713de068293cb809d",
      "marketHash": "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
      "maker": "0x63a4491dC73245E181c47BAe0ae9d6627E56dE55",
      "totalBetSize": "10000000000000000000",
      "percentageOdds": "29542732332840140000",
      "expiry": 2209006800,
      "apiExpiry": 1631233201,
      "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
      "executor": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
      "salt": "37069036490382455296196784649228360571791475783443923366499720348790829992442",
      "isMakerBettingOutcomeOne": false,
      "signature": "0x68fb16ff440c65e0306cb16a9842da362480208a9a75597d45ca722769d93e6a13c9196a2654f764bfd5c0d4c83165c0a8ffa955ae9af8afd17544b0db29eaf71c",
      "createdAt": "2021-06-04T17:42:07.303Z"
    },
    {
      "fillAmount": "0",
      "orderHash": "0xa5a30ca2251ac1431adf3d88f5734a53b78a13b2c707211eb83996bf099e3973",
      "marketHash": "0x15c5cceb3d27518241355e9f148ef96b0a178f1bcdb366dea2d0e621a9cef1fb",
      "maker": "0x63a4491dC73245E181c47BAe0ae9d6627E56dE55",
      "totalBetSize": "10000000000000000000",
      "percentageOdds": "50000000000000000000",
      "expiry": 2209006800,
      "apiExpiry": 1631233201,
      "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
      "executor": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
      "salt": "90344661128498016788545482097709376028896473001963632493180076229973632520043",
      "isMakerBettingOutcomeOne": true,
      "signature": "0x9b6c1e1d0cae584a3078f20d7bafd2031467a1cbce905027c6c970c13edef4357eeac625afe869417ffbecfb67b6672b765177d42fbda777f6b1a00962da2cc61c",
      "createdAt": "2021-06-04T17:42:07.270Z"
    }
  ]
}
```

This endpoint returns active orders on the exchange based on a few parameters

### HTTP Request

`GET https://api.sx.bet/orders`

### Query parameters

<aside class="notice">
Parameters marked with an '*' are coming soon in future release.
</aside>

| Name          | Required | Type     | Description                                               |
| ------------- | -------- | -------- | --------------------------------------------------------- |
| marketHashes  | false    | string[] | Only get orders for these market hashes. Comma separated. |
| baseToken     | false    | string   | Only get orders denominated in this base token            |
| maker         | false    | string   | Only get orders for this market maker                     |
| sportXeventId | false    | string   | Only get orders for this event ID                         |
| orderHashes*   | false    | string[] | Only get orders for these order hashes. Comma separated. |
| page*   | false    | integer | Which page to query for paginated queries, min 0 |
| perPage*   | false    | integer | How many per page for paginated queries, max 1000 |
| sortBy*   | false    | string | Which field to sort by, possible values: ["fill_amount", "total_bet_size", "percentage_odds", "api_expiry", "created_at", "updated_at"], default: "created_at" |
| sortAsc*   | false    | boolean | Sort direction, default: true |

<aside class="notice">
One of `marketHashes` or `maker` is required.
</aside>

<aside class="notice">
Only one of `marketHashes` and `sportXEventId` can be present.
</aside>

### Response format

| Name                     | Type    | Description                                                                                                                                                                                                                                                                                                                                    |
| ------------------------ | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fillAmount               | string  | How much this order has been filled in Ethereum units up to a max of `totalBetSize`. See [the token section](#tokens) of how to convert this into nominal amounts                                                                                                                                                                              |
| orderHash                | string  | A unique identifier for this order                                                                                                                                                                                                                                                                                                             |
| marketHash               | string  | The market corresponding to this order                                                                                                                                                                                                                                                                                                         |
| maker                    | string  | The market maker for this order                                                                                                                                                                                                                                                                                                                |
| totalBetSize             | string  | The total size of this order in Ethereum units. See the [the token section](#tokens) section for how to convert this into nominal amounts.                                                                                                                                                                                                     |
| percentageOdds           | string  | The odds that the `maker` receives in the sx.bet protocol format. To convert to an implied odds divide by 10^20. To convert to the odds that the taker would receive if this order would be filled in implied format, use the formula `takerOdds=1-percentageOdds/10^20`. See the [unit conversion section](#bookmaker-odds) for more details. |
| expiry                   | number  | Deprecated: the time in unix seconds after which this order is no longer valid. After deprecation, this field is always 2209006800 (2040)                                                                                                                                                                                                      |
| apiExpiry                | number  | The time in unix seconds after which this order is no longer valid.                                                                                                                                                                                                                                                                            |
| baseToken                | string  | The base token this order is denominated in                                                                                                                                                                                                                                                                                                    |
| executor                 | string  | The address permitted to execute on this order. This is set to the sx.bet exchange                                                                                                                                                                                                                                                             |
| salt                     | string  | A random number to differentiate identical orders                                                                                                                                                                                                                                                                                              |
| isMakerBettingOutcomeOne | boolean | `true` if the maker is betting outcome one (and hence taker is betting outcome two if filled)                                                                                                                                                                                                                                                  |
| signature                | string  | Signature of the maker on this order                                                                                                                                                                                                                                                                                                           |
| sportXeventId            | string  | The event related to this order                                                                                                                                                                                                                                                                                                                |

### Error Responses

| Error Code                              | Description                                            |
| --------------------------------------- | ------------------------------------------------------ |
| RATE_LIMIT_ORDER_REQUEST_MARKET_COUNT   | More than 1000 `marketHashes` queried                  |
| BOTH_SPORTXEVENTID_MARKETHASHES_PRESENT | Can only send one of `marketHashes` or `sportXEventId` |

<aside class="notice">
Note that <code>totalBetSize</code> and <code>fillAmount</code> are from *the perspective of the market maker*. <code>totalBetSize</code> can be thought of as the maximum amount of tokens the maker will be putting into the pot if the order was fully filled. <code>fillAmount</code> can be thought of as how many tokens the maker has already put into the pot. To compute how much space there is left from the taker's perspective, you can use the formula <code>remainingTakerSpace = (totalBetSize - fillAmount) * 10^20 / percentageOdds - (totalBetSize - fillAmount)</code>
</aside>

## Get best odds

```shell
curl --location --request GET 'https://api.sx.bet/orders/odds/best'
```

> The above command returns JSON structured like this

```json
{
  "status": "success",
  "data": {
      "bestOdds": [
        {
          "marketHash": "0xddaf2ef56d0db2317cf9a1e1dde3de2f2158e28bee55fe35a684389f4dce0cf6",
          "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
          "outcomeOne": {
            "percentageOdds": "57750000000000000000",
            "updatedAt": 1747408399544
          },
          "outcomeTwo": {
            "percentageOdds": "34000000000000000000",
            "updatedAt": 1747408399544
          }
        },
        {
          "marketHash": "0x7aa1477c99725a75f24d7e521bd02f247c4ca7319e0d4ad4a8350eb170b2eeae",
          "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
          "outcomeOne": {
            "percentageOdds": "9250000000000000000",
            "updatedAt": 1747414402993
          },
          "outcomeTwo": {
            "percentageOdds": "82500000000000000000",
            "updatedAt": 1747414402993
          }
        }
      ]
  }
}
```

This endpoint returns the best available odds for the specified baseToken and marketHashes or leagueIds.

### HTTP Request

`GET https://api.sx.bet/orders/odds/best`

### Query parameters

| Name          | Required | Type     | Description                                               |
| ------------- | -------- | -------- | --------------------------------------------------------- |
| marketHashes  | true    | string[] | Only get best odds for these market hashes. Comma separated. |
| leagueIds  | true    | string[] | Only get best odds for these league ids. Comma separated. |
| baseToken     | true    | string   | Only get best odds denominated in this base token.            |


<aside class="notice">
One of `marketHashes` or `leagueIds` is required.
</aside>

<aside class="notice">
Only one of `marketHashes` and `leagueIds` can be present.
</aside>

### Response format

| Name                     | Type    | Description                                                                                                                                                                                                                                                                                                                                    |
| ------------------------ | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| marketHash               | string  | The resulting market for the given best odds query                                                                                                                                                                                                                                                                                                         |
| baseToken                    | string  | The baseToken for the given best odds query                                                                                                                                                                                                                                                                                                                |
| outcomeOne             | object  | An object representing outcome one, including the best available percentage odds as `percentageOdds` (string) and the last update time as `updatedAt` (numerical timestamp in milliseconds)                                                                                                                                                                                                     |
| outcomeTwo             | object  | An object representing outcome two, including the best available percentage odds as `percentageOdds` (string) and the last update time as `updatedAt` (numerical timestamp in milliseconds)                                                                                                                                                                                                     |

## Enabling betting

```javascript
import { MaxUint256 } from "ethers/constants";
import { Contract } from "ethers";
import { JsonRpcProvider } from "ethers/providers";

const walletAddress = process.env.WALLET_ADDRESS;
const tokenAddress = process.env.TOKEN_ADDRESS;
const tokenTransferProxyAddress = process.env.TOKEN_TRANSFER_PROXY_ADDRESS;
const provider = new providers.JsonRpcProvider(process.env.RPC_URL); // find this under the 'references' section
const wallet = new Wallet(process.env.PRIVATE_KEY).connect(provider);
const tokenContract = new Contract(
  tokenAddress,
  [
    {
      constant: false,
      inputs: [
        { internalType: "address", name: "usr", type: "address" },
        { internalType: "uint256", name: "wad", type: "uint256" },
      ],
      name: "approve",
      outputs: [{ internalType: "bool", name: "", type: "bool" }],
      payable: false,
      stateMutability: "nonpayable",
      type: "function",
    },
  ],
  wallet
);
await tokenContract.approve(tokenTransferProxyAddress, MaxUInt256, {
  gasLimit: 100000,
});
```

To enable betting (filling or posting orders), you need to approve the `TokenTransferProxy` contract for each token for which you wish to trade. Otherwise, any endpoints that create/cancel or fill orders will fail. For example if you want to trade with both ETH and USDC, you'll need to approve the contract twice, once for each token. The address of the `TokenTransferProxy` is available at `https://api.sx.bet/metadata` and the address of each token is given in [the tokens section](#tokens)

If you don't wish to do this programmatically, you can simply go to `https://sx.bet`, make a test bet with the account and token you'll be using, and you will be good to go.

If you want to do it programmatically, see the code sample on the right. Note you will need a tiny bit of SX to make this transaction.

<aside class="notice">
Your assets must be on SX Network to place or fill orders via the API.
</aside>

## Post a new order

```shell
curl --location --request POST 'https://api.sx.bet/orders/new' \
--header 'Content-Type: application/json' \
--data-raw '{
    "orders": [
        {
            "marketHash": "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
            "maker": "0x6F75bA6c90E3da79b7ACAfc0fb9cf3968aa4ee39",
            "totalBetSize": "21600000000000000000",
            "percentageOdds": "47846889952153115000",
            "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
            "apiExpiry": 1631359800,
            "expiry": 2209006800,
            "executor": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
            "isMakerBettingOutcomeOne": true,
            "signature": "0x50b00e7994b0656f78701537296444bccba2a7e4d46a84ff26c8ca48cb66774c76faa893be293412959779900232065c8236e489158070777d7a3e1a37d911811b",
            "salt": "61882422358902283358380622686147595792242782952753619716150366288606659190035"
        }
    ]
}'
```

```typescript
import { BigNumber, utils, providers, Wallet } from "ethers";

const order = {
  marketHash:
    "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
  maker: "0x6F75bA6c90E3da79b7ACAfc0fb9cf3968aa4ee39",
  totalBetSize: BigNumber.from("21600000000000000000").toString(),
  percentageOdds: BigNumber.from("47846889952153115000").toString(),
  baseToken: "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
  apiExpiry: 1631233201,
  expiry: 2209006800,
  executor: "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
  isMakerBettingOutcomeOne: true,
  salt: BigNumber.from(utils.randomBytes(32)).toString(),
};

const orderHash = utils.arrayify(
  utils.solidityKeccak256(
    [
      "bytes32",
      "address",
      "uint256",
      "uint256",
      "uint256",
      "uint256",
      "address",
      "address",
      "bool",
    ],
    [
      order.marketHash,
      order.baseToken,
      order.totalBetSize,
      order.percentageOdds,
      order.expiry,
      order.salt,
      order.maker,
      order.executor,
      order.isMakerBettingOutcomeOne,
    ]
  )
);

// Example shown here with an ethers.js wallet if you're interacting with the exchange using a private key
const wallet = new Wallet(process.env.PRIVATE_KEY);
const signature = await wallet.signMessage(orderHash);

// Example shown here if you're interacting with the exchange using an injected web3 provider such as metamask
const provider = new providers.Web3Provider(window.ethereum);
const signer = provider.getSigner();
const signature = await signer.signMessage(orderHash);

const signedOrder = { ...order, signature };

const result = await fetch("https://api.sx.bet/orders/new", {
  method: "POST",
  body: JSON.stringify({ orders: [signedOrder] }),
  headers: { "Content-Type": "application/json" },
});

// Odds ladder testing

import { BigNumber } from "bignumber.js";
import { BigNumber as EthBigNumber } from "ethers";

export const ODDS_LADDER_STEP_SIZE = 25; // (0.1% = 1, 0.5% = 5, etc)

/**
 * Check if the odds are valid, i.e., in one of the allowed steps
 * @param odds Odds to check
 */
export function checkOddsLadderValid(
  odds: EthBigNumber,
  stepSizeOverride?: number
) {
  // Logic:
  // 100% = 10^20
  // 10% = 10^19
  // 1% = 10^18
  // 0.1% = 10^17
  return odds
    .mod(EthBigNumber.from(10).pow(16).mul(ODDS_LADDER_STEP_SIZE))
    .eq(0);
}

/**
 * Rounds odds to the nearest step.
 * @param odds Odds to round.
 */
export function roundDownOddsToNearestStep(
  odds: EthBigNumber,
  stepSizeOverride?: number
) {
  const step = EthBigNumber.from(10).pow(16).mul(ODDS_LADDER_STEP_SIZE);
  const bnStep = new BigNumber(step.toString());
  const bnOdds = new BigNumber(odds.toString());
  const firstPassDivision = bnOdds.dividedBy(bnStep).toFixed(0, 3);
  return EthBigNumber.from(firstPassDivision).mul(step);
}
```

> The above command returns JSON structured like this

```json
{
  "status": "success",
  "data": {
    "orders": [
      "0x7a9d420551c4a635849013dd908f7894766e97aee25fe656d0c5ac857e166fac"
    ]
  }
}
```

This endpoint offers new orders on the exchange (market making). Offering orders does not cost any fee.

Note you can offer as many orders as you wish, provided your total exposure for each token (as measured by `totalBetSize - fillAmount`) remains under your wallet balance. If your wallet balance dips under your total exposure, orders will be removed from the book until it reaches the minimum again.

<aside class="notice">
Your assets must be on SX Network to place orders.
</aside>

<aside class="warning">
If the API finds that your balance is consistently below your total exposure requiring orders to be cancelled, your account may be temporarily restricted. 
</aside>

To offer bets on sx.bet via the API, make sure you first enable betting by following the steps [here](#enabling-betting).

We enforce an odds ladder to prevent diming. Your offer, in implied odds, must fall on one of the steps on the ladder. Currently, that is set to intervals of 0.25%, meaning that your offer cannot fall between the steps. An offer of 50.25% would be valid, but an offer of 50.05% would not. You can check if your odds would fall on the ladder by taking the modulus of your odds and 2.5 \* 10 ^ 17 and checking if it's equal to 0. See the bottom of the JavaScript tab for a sample on how to do this, and how to round your odds to the nearest step.

You can get the current interval from `GET /metadata`. It will spit out a number from 10 to 100, where 10 = 0.10%, and 25 = 0.25%

<aside class="warning">
Odds not on the ladder will be rejected and your order(s) will not be posted. 
</aside>

### HTTP Request

`POST https://api.sx.bet/orders/new`

### Request payload parameters

| Name   | Required | Type             | Description            |
| ------ | -------- | ---------------- | ---------------------- |
| orders | true     | SignedNewOrder[] | The new orders to post |

A `SignedNewOrder` object looks like this

| Name                     | Type    | Description                                                                                                       |
| ------------------------ | ------- | ----------------------------------------------------------------------------------------------------------------- |
| marketHash               | string  | The market you wish to place this order under                                                                     |
| maker                    | string  | The ethereum address offering the bet                                                                             |
| baseToken                | string  | The token this order is denominated in                                                                            |
| totalBetSize             | string  | The total bet size of the order in Ethereum units.                                                                |
| percentageOdds           | string  | The odds _the maker will be receiving_ as this order gets filled. Must be on the odds ladder or will be rejected. |
| expiry                   | number  | Deprecated. Time in UNIX seconds after which this order is no longer valid. Must always be 2209006800.            |
| apiExpiry                | number  | Time in UNIX seconds after which this order is no longer valid.                                                   |
| executor                 | string  | The sx.bet executor address. See the [metadata section](#get-metadata) for where to get this address              |
| salt                     | string  | A random 32 byte string to differentiate between between orders with otherwise identical parameters               |
| isMakerBettingOutcomeOne | boolean | `true` if the maker is betting outcome one (and hence taker is betting outcome two if filled)                     |
| signature                | string  | The signature of the maker on this order payload                                                                  |

<aside class="notice">
The address in the <code>maker</code> field must match the account being used to create the signature!
</aside>

### Response format

| Name     | Type     | Description                                            |
| -------- | -------- | ------------------------------------------------------ |
| status   | string   | `success` or `failure` if the request succeeded or not |
| data     | object   | The response data                                      |
| > orders | string[] | The order hashes corresponding to the new orders       |

<aside class="notice">
Note that <code>totalBetSize</code> is from *the perspective of the market maker*. <code>totalBetSize</code> can be thought of as the maximum amount of tokens the maker (you) will be putting into the pot if the order was fully filled. This is the maximum amount you will risk.
</aside>

### Error Responses

| Error Code                        | Description                                                        |
| --------------------------------- | ------------------------------------------------------------------ |
| TOO_MANY_DIFFERENT_MARKETS        | More than 3 different markets queried                              |
| ORDERS_MUST_HAVE_IDENTICAL_MARKET | All orders must be for the same network, either `SXN` or `SXR`     |
| BAD_BASE_TOKEN                    | All orders must be for the same base token, either `USDC` or `WSX` |

## Cancel individual orders

```shell
curl --location --request POST 'https://api.sx.bet/orders/cancel/v2' \
--header 'Content-Type: application/json' \
--data-raw '{
    "orderHashes": [
        "0x335d3dbd0621f0f6da90d1a58269e71b2fb5e91193dca75a0b90396cccb63001"
    ],
    "signature": "0x1763cb98a069657cb778fdc295eac48741b957bfe58e54f7f9ad03c6c1ca3d053d9ca2e6957af794991217752b69cb9aa4ac9330395c92e24c8c25ec19220e5a1b",
    "salt": "0x6845028402f518a1c90770554a71017cd434ae9f2c09aa56c9560835c1929650",
    "maker": "0xe087299AE9Acd0133d6D1544A97Bb0EEe24a2671",
    "timestamp": 1643897553
}'
```

```javascript
import { signTypedData, SignTypedDataVersion } from "@metamask/eth-sig-util";
import { randomBytes } from "@ethersproject/random";

// Example is shown using a private key

const privateKey = process.env.PRIVATE_KEY;
const bufferPrivateKey = Buffer.from(privateKey.substring(2), "hex");
const orderHashes = [
  "0x4ead6ef92741cd0b6e1ea32cb1d9586a85165e8bd780ab6f897992428c357bf1",
];
const salt = `0x${Buffer.from(randomBytes(32)).toString("hex")}`;
const timestamp = Math.floor(new Date().getTime() / 1000);
const wallet = new Wallet(privateKey);

function getCancelOrderEIP712Payload(orderHashes, salt, timestamp, chainId) {
  const payload = {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "chainId", type: "uint256" },
        { name: "salt", type: "bytes32" },
      ],
      Details: [
        { name: "orderHashes", type: "string[]" },
        { name: "timestamp", type: "uint256" },
      ],
    },
    primaryType: "Details",
    domain: {
      name: "CancelOrderV2SportX",
      version: "1.0",
      chainId,
      salt,
    },
    message: { orderHashes, timestamp },
  };
  return payload;
}

const payload = getCancelOrderEIP712Payload(orderHashes, salt, timestamp, chainId);

const signature = signTypedData({
  privateKey: bufferPrivateKey, 
  data: payload,
  version: SignTypedDataVersion.V4,
});

const apiPayload = {
  signature,
  orderHashes,
  salt,
  maker: wallet.address,
  timestamp,
};

const result = await fetch("https://api.sx.bet/orders/cancel/v2", {
  method: "POST",
  body: JSON.stringify(apiPayload),
  headers: { "Content-Type": "application/json" },
});
```

> The above command returns json structured like this

```json
{
  "status": "success",
  "data": {
    "cancelledCount": 1,
    "orders": [
      {
        "orderHash": "0xc4fad4101eac3d72a7d4166df05534edd5479ec705307624498d6ec60336ef45",
        "pendingFills": [
          {
              "fillHash": "0xf691c9dfb100d125503c0b4dad944f15d711eaf22108c6dacc5077a274b35821",
              "pendingFillAmount": "106995918"
          }
        ]
      }
    ]
  }
}
```

This endpoint cancels existing orders on the exchange that you placed as a market maker. If passed orders that do not exist, they simply fail silently while the others will succeed.

### HTTP Request

`POST https://api.sx.bet/orders/cancel/v2`

### Request payload parameters

| Name        | Required | Type     | Description                                                                                                                                            |
| ----------- | -------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| orderHashes | true     | string[] | The order hashes to cancel                                                                                                                             |
| signature   | true     | string   | The EIP712 signature on the cancel order payload. See the [EIP712 signing section](#eip712-signing) for more details on how to compute this signature. |
| salt        | required | string   | A random 32 bytes hex string to protect against replay                                                                                                 |
| maker       | required | true     | The account from which you are cancelling orders                                                                                                       |
| timestamp   | required | true     | The current timestamp in UNIX seconds to protect against replay                                                                                        |

### Response format

| Name             | Type             | Description                                                        |
| ---------------- | ---------------- | ------------------------------------------------------------------ |
| status           | string           | `success` or `failure` if the request succeeded or not             |
| data             | object           | The response data                                                  |
| > cancelledCount | number           | How many orders were cancelled, of the orders passed               |
| > orders?        | CancelledOrder[] | An array of Cancelled Order objects. Omitted if cancel count is 0. |

A `CancelledOrder` object looks like this

| Name             | Type           | Description                                                                          |
| -------------| -------------- | ------------------------------------------------------------------------------------ |
| orderHash    | string         | Cancelled order hash                                                                 |
| pendingFills | PendingFill[]  | The pending fills awaiting confirmation on chain. Expected to succeed and fill order.|

A `PendingFill` object looks like this

| Name              | Type   | Description                                                   |
| ----------------- | ------ | ------------------------------------------------------------- |
| fillHash          | string | The fill hash which is pending                                |
| pendingFillAmount | string | The amount of the order that this fill is attempting to fill. |

### Error Responses

| Error Code                       | Description                            |
| -------------------------------- | -------------------------------------- |
| CANCEL_REQUEST_ALREADY_PROCESSED | This cancellation is already processed |

## Cancel event orders

```shell
curl --location --request POST 'https://api.sx.bet/orders/cancel/event' \
--header 'Content-Type: application/json' \
--data-raw '{
    "sportXEventId": "L1234123",
    "signature": "0x1763cb98a069657cb778fdc295eac48741b957bfe58e54f7f9ad03c6c1ca3d053d9ca2e6957af794991217752b69cb9aa4ac9330395c92e24c8c25ec19220e5a1b",
    "salt": "0x6845028402f518a1c90770554a71017cd434ae9f2c09aa56c9560835c1929650",
    "maker": "0xe087299AE9Acd0133d6D1544A97Bb0EEe24a2671",
    "timestamp": 1643898624
}'
```

```javascript
import { signTypedData, SignTypedDataVersion } from "@metamask/eth-sig-util";
import { randomBytes } from "@ethersproject/random";
import { Wallet } from "@ethersproject/wallet";

// Example is shown using a private key

const privateKey = process.env.PRIVATE_KEY;
const bufferPrivateKey = Buffer.from(privateKey.substring(2), "hex");
const sportXeventId = "L1231231";
const salt = `0x${Buffer.from(randomBytes(32)).toString("hex")}`;
const timestamp = Math.floor(new Date().getTime() / 1000);
const wallet = new Wallet(privateKey);

function getCancelOrderEventsEIP712Payload(
  sportXEventId,
  salt,
  timestamp,
  chainId
) {
  const payload = {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "chainId", type: "uint256" },
        { name: "salt", type: "bytes32" },
      ],
      Details: [
        { name: "sportXeventId", type: "string" },
        { name: "timestamp", type: "uint256" },
      ],
    },
    primaryType: "Details",
    domain: {
      name: "CancelOrderEventsSportX",
      version: "1.0",
      chainId,
      salt,
    },
    message: { sportXEventId, timestamp },
  };
  return payload;
}

const payload = getCancelOrderEventsEIP712Payload(
  sportXeventId,
  salt,
  timestamp,
  chainId
);

const signature = signTypedData({
  privateKey: bufferPrivateKey,
  data: payload,
  version: SignTypedDataVersion.V4,
});

const apiPayload = {
  signature,
  sportXeventId,
  salt,
  maker: wallet.address,
  timestamp,
};

const result = await fetch("https://api.sx.bet/orders/cancel/event", {
  method: "POST",
  body: JSON.stringify(apiPayload),
  headers: { "Content-Type": "application/json" },
});
```

> The above command returns json structured like this

```json
{
  "status": "success",
  "data": {
    "cancelledCount": 1,
    "orders": [
      {
        "orderHash": "0xc4fad4101eac3d72a7d4166df05534edd5479ec705307624498d6ec60336ef45",
        "pendingFills": [
          {
              "fillHash": "0xf691c9dfb100d125503c0b4dad944f15d711eaf22108c6dacc5077a274b35821",
              "pendingFillAmount": "106995918"
          }
        ]
      }
    ]
  }
}
```

This endpoint cancels existing orders on the exchange for a particular event that you placed as a market maker.

### HTTP Request

`POST https://api.sx.bet/orders/cancel/event`

### Request payload parameters

| Name          | Required | Type   | Description                                                                                                                                            |
| ------------- | -------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| sportXeventId | true     | string | The event for which orders should be cancelled                                                                                                         |
| signature     | true     | string | The EIP712 signature on the cancel order payload. See the [EIP712 signing section](#eip712-signing) for more details on how to compute this signature. |
| salt          | required | string | A random 32 bytes hex string to protect against replay                                                                                                 |
| maker         | required | true   | The account from which you are cancelling orders                                                                                                       |
| timestamp     | required | true   | The current timestamp in UNIX seconds to protect against replay                                                                                        |

### Response format

| Name             | Type             | Description                                                        |
| ---------------- | ---------------- | ------------------------------------------------------------------ |
| status           | string           | `success` or `failure` if the request succeeded or not             |
| data             | object           | The response data                                                  |
| > cancelledCount | number           | How many orders were cancelled, of the orders passed               |
| > orders?        | CancelledOrder[] | An array of Cancelled Order objects. Omitted if cancel count is 0. |

A `CancelledOrder` object looks like this

| Name             | Type           | Description                                                                          |
| -------------| -------------- | ------------------------------------------------------------------------------------ |
| orderHash    | string         | Cancelled order hash                                                                 |
| pendingFills | PendingFill[]  | The pending fills awaiting confirmation on chain. Expected to succeed and fill order.|

A `PendingFill` object looks like this

| Name              | Type   | Description                                                   |
| ----------------- | ------ | ------------------------------------------------------------- |
| fillHash          | string | The fill hash which is pending                                |
| pendingFillAmount | string | The amount of the order that this fill is attempting to fill. |

### Error Responses

| Error Code                       | Description                            |
| -------------------------------- | -------------------------------------- |
| CANCEL_REQUEST_ALREADY_PROCESSED | This cancellation is already processed |

## Cancel all orders

```shell
curl --location --request POST 'https://api.sx.bet/orders/cancel/all' \
--header 'Content-Type: application/json' \
--data-raw '{
    "signature": "0x1763cb98a069657cb778fdc295eac48741b957bfe58e54f7f9ad03c6c1ca3d053d9ca2e6957af794991217752b69cb9aa4ac9330395c92e24c8c25ec19220e5a1b",
    "salt": "0x6845028402f518a1c90770554a71017cd434ae9f2c09aa56c9560835c1929650",
    "maker": "0xe087299AE9Acd0133d6D1544A97Bb0EEe24a2671",
    "timestamp": 1643898624
}'
```

```javascript
import { signTypedData, SignTypedDataVersion } from "@metamask/eth-sig-util";
import { randomBytes } from "@ethersproject/random";
import { Wallet } from "@ethersproject/wallet";

// Example is shown using a private key

const privateKey = process.env.PRIVATE_KEY;
const bufferPrivateKey = Buffer.from(privateKey.substring(2), "hex");
const salt = `0x${Buffer.from(randomBytes(32)).toString("hex")}`;
const timestamp = Math.floor(new Date().getTime() / 1000);
const wallet = new Wallet(privateKey);

function getCancelAllOrdersEIP712Payload(salt, timestamp, chainId) {
  const payload = {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "chainId", type: "uint256" },
        { name: "salt", type: "bytes32" },
      ],
      Details: [{ name: "timestamp", type: "uint256" }],
    },
    primaryType: "Details",
    domain: {
      name: "CancelAllOrdersSportX",
      version: "1.0",
      chainId,
      salt,
    },
    message: { timestamp },
  };
  return payload;
}

const payload = getCancelOrderEventsEIP712Payload(salt, timestamp, chainId);

const signature = signTypedData({
  privateKey: bufferPrivateKey,
  data: payload,
  version: SignTypedDataVersion.V4,
});

const apiPayload = {
  signature,
  salt,
  maker: wallet.address,
  timestamp,
};

const result = await fetch("https://api.sx.bet/orders/cancel/all", {
  method: "POST",
  body: JSON.stringify(apiPayload),
  headers: { "Content-Type": "application/json" },
});
```

> The above command returns json structured like this

```json
{
  "status": "success",
  "data": {
    "cancelledCount": 1,
    "orders": [
      {
        "orderHash": "0xc4fad4101eac3d72a7d4166df05534edd5479ec705307624498d6ec60336ef45",
        "pendingFills": [
          {
              "fillHash": "0xf691c9dfb100d125503c0b4dad944f15d711eaf22108c6dacc5077a274b35821",
              "pendingFillAmount": "106995918"
          }
        ]
      }
    ]
  }
}
```

This endpoint cancels ALL existing orders on the exchange that you placed as a market maker.

### HTTP Request

`POST https://api.sx.bet/orders/cancel/all`

### Request payload parameters

| Name      | Required | Type   | Description                                                                                                                                            |
| --------- | -------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| signature | true     | string | The EIP712 signature on the cancel order payload. See the [EIP712 signing section](#eip712-signing) for more details on how to compute this signature. |
| salt      | required | string | A random 32 bytes hex string to protect against replay                                                                                                 |
| maker     | required | true   | The account from which you are cancelling orders                                                                                                       |
| timestamp | required | true   | The current timestamp in UNIX seconds to protect against replay.                                                                                       |

### Response format

| Name             | Type             | Description                                                        |
| ---------------- | ---------------- | ------------------------------------------------------------------ |
| status           | string           | `success` or `failure` if the request succeeded or not             |
| data             | object           | The response data                                                  |
| > cancelledCount | number           | How many orders were cancelled, of the orders passed               |
| > orders?        | CancelledOrder[] | An array of Cancelled Order objects. Omitted if cancel count is 0. |

A `CancelledOrder` object looks like this

| Name             | Type           | Description                                                                          |
| -------------| -------------- | ------------------------------------------------------------------------------------ |
| orderHash    | string         | Cancelled order hash                                                                 |
| pendingFills | PendingFill[]  | The pending fills awaiting confirmation on chain. Expected to succeed and fill order.|

A `PendingFill` object looks like this

| Name              | Type   | Description                                                   |
| ----------------- | ------ | ------------------------------------------------------------- |
| fillHash          | string | The fill hash which is pending                                |
| pendingFillAmount | string | The amount of the order that this fill is attempting to fill. |

### Error Responses

| Error Code                       | Description                            |
| -------------------------------- | -------------------------------------- |
| CANCEL_REQUEST_ALREADY_PROCESSED | This cancellation is already processed |

## Filling orders v1

<aside class="notice">
Deprecating soon! See <a href="#filling-orders-v2">Filling orders v2</a> for improved fill endpoint.
</aside>

```shell
curl --location --request POST 'https://api.sx.bet/orders/fill' \
--header 'Content-Type: application/json' \
--data-raw '{"orderHashes":["0x863a2288a640e1bb722da2ee7a6f323ea28caee8ac681d320534d0e7f2e849de","0x001f676d68baf85310145f85bc5aeba64108b234607b4fae25c704069ca8464a"],"takerAmounts":["10000000000000000000","10000000000000000000"],"taker":"0xa3bBFaB3645B2Dd4296cADc451d74574CD47Ba1a","takerSig":"0x09d2603a8c8646221d6972b04a5cdd8b13d6326a267329825567a25a5e63606b07b97c84640bfb3ee4a5053083ce178d9e0c9cbdf1b1dfd519fda0594fae30dc1c","fillSalt":"69231297238279245345865414293427982207908612843136003245427437324972455931243","action":"N/A","market":"N/A","betting":"N/A","stake":"N/A","odds":"N/A","returning":"N/A"}'
```

```javascript
import { signTypedData, SignTypedDataVersion } from "@metamask/eth-sig-util";
import {
  BigNumber,
  constants,
  Contract,
  providers,
  utils,
  Wallet,
} from "ethers";
import { randomBytes } from "ethers/lib/utils";
import dayjs from "dayjs";

async function fillOrder() {
  const privateKey = process.env.PRIVATE_KEY;
  const takerAddress = process.env.TAKER_ADDRESS;
  const tokenAddress = process.env.TOKEN_ADDRESS;

  // get the following from https://api.sx.bet/metadata
  const tokenTransferProxyAddress = process.env.TOKEN_TRANSFER_PROXY_ADDRESS;
  const EIP712FillHasherAddress = process.env.EIP712_FILL_HASHER_ADDRESS;
  const chainId = process.env.CHAIN_ID; // 4162 in production
  const domainVersion = process.env.DOMAIN_VERSION;

  const bufferPrivateKey = Buffer.from(privateKey!.substring(2), "hex");
  const wallet = new Wallet(privateKey).connect(
    new providers.JsonRpcProvider(process.env.RPC_URL) // find this under the 'references' section
  );
  const takerAmounts = ["10000000000000000000", "10000000000000000000"];
  const fillSalt = BigNumber.from(randomBytes(32)).toString();
  const approvalAmount = constants.MaxUint256;
  const tokenContract = new Contract(
    tokenAddress,
    [
      {
        constant: false,
        inputs: [
          { internalType: "address", name: "usr", type: "address" },
          { internalType: "uint256", name: "wad", type: "uint256" },
        ],
        name: "approve",
        outputs: [{ internalType: "bool", name: "", type: "bool" }],
        payable: false,
        stateMutability: "nonpayable",
        type: "function",
      },
      {
        inputs: [
          {
            internalType: "address",
            name: "owner",
            type: "address",
          },
        ],
        name: "nonces",
        outputs: [
          {
            internalType: "uint256",
            name: "",
            type: "uint256",
          },
        ],
        stateMutability: "view",
        type: "function",
        constant: true,
      },
      {
        inputs: [],
        name: "name",
        outputs: [
          {
            internalType: "string",
            name: "",
            type: "string"
          }
        ],
        stateMutability: "view",
        type: "function",
        constant: true
      }
    ],
    wallet
  );

  let nonce: BigNumber = await tokenContract.nonces(takerAddress);
  const tokenName: string = await tokenContract.name();

  const ordersToFill = [
    {
      fillAmount: "0",
      orderHash:
        "0x863a2288a640e1bb722da2ee7a6f323ea28caee8ac681d320534d0e7f2e849de",
      marketHash:
        "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
      maker: "0x63a4491dC73245E181c47BAe0ae9d6627E56dE55",
      totalBetSize: "120000000000000000000",
      percentageOdds: "68860772772306080000",
      expiry: 2209006800,
      apiExpiry: 1631233201,
      baseToken: "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
      executor: "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
      salt:
        "64542697517744547417546237340530363903382582642857122744382059379852833736063",
      isMakerBettingOutcomeOne: true,
      signature:
        "0xa58255f9f7bb8a2698d66f9931a3d4ebe2e5605299a57d78b7c048f26585fdb5144b16bb930ad564f2e2819f66c8c20c2c076d8951728d8242481d58af221fc51b",
      createdAt: "2021-06-24T21:44:51.355Z",
    },
    {
      fillAmount: "0",
      orderHash:
        "0x001f676d68baf85310145f85bc5aeba64108b234607b4fae25c704069ca8464a",
      marketHash:
        "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
      maker: "0x63a4491dC73245E181c47BAe0ae9d6627E56dE55",
      totalBetSize: "120000000000000000000",
      percentageOdds: "27138321995464855000",
      expiry: 2209006800,
      apiExpiry: 1631233201,
      baseToken: "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
      executor: "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
      salt:
        "33394198022904122521460365691253625674733505262618329029186356280403872887283",
      isMakerBettingOutcomeOne: false,
      signature:
        "0xb52be3279a092823bb46b3bd9a397bef2a06eda95a519718992ea88d73a4375874728cb7c5f6527b67195e44f3f0f0d29956dc05e18e775547d8f2faf3d4bd001c",
      createdAt: "2021-06-24T21:44:51.374Z",
    },
  ];

  const signingPayload = {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "chainId", type: "uint256" },
        { name: "verifyingContract", type: "address" },
      ],
      Details: [
        { name: "action", type: "string" },
        { name: "market", type: "string" },
        { name: "betting", type: "string" },
        { name: "stake", type: "string" },
        { name: "odds", type: "string" },
        { name: "returning", type: "string" },
        { name: "fills", type: "FillObject" },
      ],
      FillObject: [
        { name: "orders", type: "Order[]" },
        { name: "makerSigs", type: "bytes[]" },
        { name: "takerAmounts", type: "uint256[]" },
        { name: "fillSalt", type: "uint256" },
        { name: "beneficiary", type: "address" },
        { name: "beneficiaryType", type: "uint8" },
        { name: "cashOutTarget", type: "bytes32" },
      ],
      Order: [
        { name: "marketHash", type: "bytes32" },
        { name: "baseToken", type: "address" },
        { name: "totalBetSize", type: "uint256" },
        { name: "percentageOdds", type: "uint256" },
        { name: "expiry", type: "uint256" },
        { name: "salt", type: "uint256" },
        { name: "maker", type: "address" },
        { name: "executor", type: "address" },
        { name: "isMakerBettingOutcomeOne", type: "bool" },
      ],
    },
    primaryType: "Details",
    domain: {
      name: "SX Bet",
      version: domainVersion,
      chainId: chainId,
      verifyingContract: EIP712FillHasherAddress,
    },
    message: {
      action: "N/A",
      market: "N/A",
      betting: "N/A",
      stake: "N/A",
      odds: "N/A",
      returning: "N/A",
      fills: {
        makerSigs: ordersToFill.map((order) => order.signature),
        orders: ordersToFill.map((order) => ({
          marketHash: order.marketHash,
          baseToken: order.baseToken,
          totalBetSize: order.totalBetSize.toString(),
          percentageOdds: order.percentageOdds.toString(),
          expiry: order.expiry.toString(),
          salt: order.salt.toString(),
          maker: order.maker,
          executor: order.executor,
          isMakerBettingOutcomeOne: order.isMakerBettingOutcomeOne,
        })),
        takerAmounts,
        fillSalt,
        beneficiary: constants.AddressZero,
        beneficiaryType: 0,
        cashOutTarget: constants.HashZero,
      },
    },
  };

  const approveProxySigningPayload = {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "chainId", type: "uint256" },
        { name: "verifyingContract", type: "address" },
      ],
      Permit: [
        { name: "owner", type: "address" },
        { name: "spender", type: "address" },
        { name: "value", type: "uint256" },
        { name: "nonce", type: "uint256" },
        { name: "deadline", type: "uint256" },
      ],
    },
    domain: {
      name: tokenName,
      version: "1",
      chainId: chainId,
      verifyingContract: tokenAddress,
    },
    message: {
      owner: takerAddress,
      spender: tokenTransferProxyAddress,
      value: approvalAmount,
      nonce: nonce.toNumber(),
      deadline: dayjs().add(2, "hour").unix(),
    },
    primaryType: "Permit",
  };

  const approveProxySignature = signTypedData({
    privateKey: bufferPrivateKey,
    data: approveProxySigningPayload,
    version: SignTypedDataVersion.V4,
  });

  const signature = signTypedData({
    privateKey: bufferPrivateKey,
    data: signingPayload,
    version: SignTypedDataVersion.V4,
  });

  const apiPayload = {
    orderHashes: ordersToFill.map((order) => order.orderHash),
    takerAmounts,
    taker: takerAddress,
    takerSig: signature,
    fillSalt,
    action: "N/A",
    market: "N/A",
    betting: "N/A",
    stake: "N/A",
    odds: "N/A",
    returning: "N/A",
    approveProxyPayload: {
      owner: takerAddress,
      spender: tokenTransferProxyAddress,
      tokenAddress,
      amount: approvalAmount.toString(),
      signature: approveProxySignature,
    },
  };

  const response = await fetch(`https://api.sx.bet/orders/fill`, {
    method: "POST",
    body: JSON.stringify(apiPayload),
    headers: { "Content-Type": "application/json" },
  });
}
```

> The above command returns json structured like this

```json
{
  "status": "success",
  "data": {
    "fillHash": "0x840763ae29b7a6adfa0e315afa47be30cdebd5b793d179dc07dc8fc4f0034965"
  }
}
```

This endpoint fills orders on the exchange. Multiple orders can be filled at once and no gas is paid as this is a meta transaction submitted by the API itself.

Note that there are built in betting delays based on the below chart. This is added to guard against toxic flow and high spikes in latency from the bookmaker's side. It is effectively protection for the bookmaker. If the odds change within that delay time, the order will be cancelled and an error will be thrown.

**PREGAME**

| Sport                | Delay ( in seconds ) |
| -------------------- | -------------------- |
| Default (all sports) | 0.5                  |

**LIVE**

| Sport               | Delay ( in seconds ) |
| ------------------- | -------------------- |
| Baseball            | 12                   |
| Football            | 10                   |
| Tennis              | 10                   |
| Soccer              | 10                   |
| Basketball          | 8                    |
| Hockey              | 8                    |
| Default (all other) | 8                    |

To fill orders on sx.bet via the API, make sure you first enable betting by following the steps [here](#enabling-betting)

<aside class="notice">
Your assets must be on SX Network to place bets.
</aside>

### HTTP Request

`POST https://api.sx.bet/orders/fill`

### Request payload parameters

| Name                | Required | Type                    | Description                                                                                                                                                                                                                                                 |
| ------------------- | -------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| action              | true     | string                  | User facing string for what action the user is taking. Can simply set to "N/A" when using the API                                                                                                                                                           |
| betting             | true     | string                  | User facing string for what bet the user is making. Can simply set to "N/A" when using the API.                                                                                                                                                             |
| fillSalt            | true     | string                  | Random 32 byte string to identify this fill. Must be the same `fillSalt` used when computing the EIP712 payload                                                                                                                                             |
| market              | true     | string                  | User facing string for what market the user is betting on. Can simply set to "N/A" when using the API                                                                                                                                                       |
| odds                | true     | string                  | User facing string for the odds the user is receiving. Can simply set to "N/A" when using the API                                                                                                                                                           |
| orderHashes         | true     | string[]                | Orders being filled. Must be the order hashes of the orders used in computing the EIP712 payload. Must be the same length as `takerAmounts`                                                                                                                 |
| returning           | true     | string                  | User facing string for what the bet wil be returning. Can simply set to "N/A" when using the API.                                                                                                                                                           |
| taker               | true     | string                  | Address of the taker taking the bet                                                                                                                                                                                                                         |
| stake               | true     | string                  | User facing string for how much the user is risking. Can simly set to "N/A" when using the API.                                                                                                                                                             |
| takerAmounts        | true     | string[]                | How much each order is being filled, ordered by index. Must be in the same order as `orderHashes`, and the same length as `orderHashes`. It also must be the same and in the same order as the `takerAmounts` array used when computing the EIP712 payload. |
| takerSig            | true     | string                  | The EIP712 signature of the `taker` on the payload. See the example of how to compute this.                                                                                                                                                                 |
| message             | true     | string                  | A user-facing message for the eip712 signing. Can be anything.                                                                                                                                                                                              |
| approveProxyPayload | false    | `ApproveSpenderPayload` | Extra object required if you wish to atomically `ERC20.approve()` prior to the bet. This can be useful from a UX point of view if you don't want the user to have to wait until the approval is mined before the bet can be submitted                       |
| affiliateAddress    | false    | string                  | Set the `taker` to a valid affiliate's address.                                                                                                                                                                                                             |

where an `ApproveSpenderPayload` looks like

| Name         | Required | Type   | Description                                                                                                                                                                                     |
| ------------ | -------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| owner        | true     | string | Address of the bettor/taker                                                                                                                                                                     |
| spender      | true     | string | Address of the contract permitted to spend tokens on behalf of the bettor/taker to bet. See the `TokenTransferProxy` address in the available at `https://api.sx.bet/metadata` for this address |
| tokenAddress | true     | string | Address of the token being used to bet. Must be the same as the token referenced in the orders being filled                                                                                     |
| amount       | true     | string | Amount of tokens to approve. Must be greater than or equal to the total tokens bet from the bettors's perspective, i.e., how many tokens are leaving the bettor's wallet                        |
| signature    | true     | string | The EIP712 signature of the this payload.                                                                                                                                                       |

### Response format

| Name       | Type   | Description                                            |
| ---------- | ------ | ------------------------------------------------------ |
| status     | string | `success` or `failure` if the request succeeded or not |
| data       | object | The response data                                      |
| fillHash | string | A unique identifier for this fill.                     |

<aside class="warning">
Note that <code>takerAmounts</code> are from *the perspective of the market maker*. <code>takerAmounts</code> can be thought of as how many tokens the maker(s) will be putting into the pot. Given an amount you as the taker want to bet, you can use the following formula to convert what value you have to use as <code>takerAmount</code> in this endpoint. <code>takerAmount = takerBetAmount * percentageOdds / (10^20 - percentageOdds)</code>
</aside>

<aside class="notice">
To convert a <code>fillAmount</code> (what the market maker pays) to what the taker will pay, you can use the formula <code>takerPayAmount = fillAmount * 10^20 / percentageOdds - fillAmount </code>. Intuitively, this is the pot size (<code>fillAmount * 10^20 / percentageOdds)</code> minus what the maker is putting in
</aside>

### Error Responses

| Error Code                 | Description                                                                  |
| ---------------------------| ---------------------------------------------------------------------------- |
| ORDERS_NOT_UNIQUE          | Only unique `orderHashes` should be sent                                     |
| INCORRECT_ARRAY_LENGTHS    | `orderHashes` and `takerAmounts` arrays are different lengths.               |
| ORDERS_DONT_EXIST          | One of the orders do not exist                                               |
| AFTER_ORDER_EXPIRY         | One of the orders have expired                                               |
| BASE_TOKENS_NOT_SAME       | All orders must be for the same `baseToken`                                  |
| MARKETS_NOT_SAME           | All orders must be for the same market                                       |
| DIRECTIONS_NOT_SAME        | All orders must be betting on the same side `isMakerBettingOutcomeOne`       |
| INVALID_ORDERS             | Order is now inactive                                                        |
| MATCH_STATE_INVALID        | The fixture for the order is in an invalid state and is not bettable anymore |
| META_TX_RATE_LIMIT_REACHED | Cannot have more than 10 meta transactions at once                           |

## Approve order fill

<aside class="notice">
Coming soon! This endpoint will be available for use soon, please follow our Discord #api-changes channel to stay up to date.
</aside>

```shell
curl --location --request POST 'https://api.sx.bet/orders/approve' \
--header 'Content-Type: application/json' \
--data-raw '{"owner":"0xa3bBFaB3645B2Dd4296cADc451d74574CD47Ba1a","spender":"0x38aef22152BC8965bf0af7Cf53586e4b0C4E9936","tokenAddress":"0x6629Ce1Cf35Cc1329ebB4F63202F3f197b3F050B","value":"100000000000","deadline":"1789692000","signature":"0x09d2603a8c8646221d6972b04a5cdd8b13d6326a267329825567a25a5e63606b07b97c84640bfb3ee4a5053083ce178d9e0c9cbdf1b1dfd519fda0594fae30dc1c"}'
```

```javascript
import { signTypedData, SignTypedDataVersion } from "@metamask/eth-sig-util";
import {
  BigNumber,
  constants,
  Contract,
  providers,
  utils,
  Wallet,
} from "ethers";
import { randomBytes } from "ethers/lib/utils";
import dayjs from "dayjs";

async function approveOrderFill() {
  const privateKey = process.env.PRIVATE_KEY;
  const tokenAddress = process.env.TOKEN_ADDRESS;

  // get the following from https://api.sx.bet/metadata
  const tokenTransferProxyAddress = process.env.TOKEN_TRANSFER_PROXY_ADDRESS;
  const chainId = process.env.CHAIN_ID; // 4162 in production
  const domainVersion = process.env.DOMAIN_VERSION;

  const bufferPrivateKey = Buffer.from(privateKey!.substring(2), "hex");
  const wallet = new Wallet(takerPrivateKey).connect(
    new providers.JsonRpcProvider(process.env.RPC_URL) // find this under the 'references' section
  );
  const approvalAmount = constants.MaxUint256;
  const tokenContract = new Contract(
    tokenAddress,
    [
      {
        constant: false,
        inputs: [
          { internalType: "address", name: "usr", type: "address" },
          { internalType: "uint256", name: "wad", type: "uint256" },
        ],
        name: "approve",
        outputs: [{ internalType: "bool", name: "", type: "bool" }],
        payable: false,
        stateMutability: "nonpayable",
        type: "function",
      },
      {
        inputs: [
          {
            internalType: "address",
            name: "owner",
            type: "address",
          },
        ],
        name: "nonces",
        outputs: [
          {
            internalType: "uint256",
            name: "",
            type: "uint256",
          },
        ],
        stateMutability: "view",
        type: "function",
        constant: true,
      },
      {
        inputs: [],
        name: "name",
        outputs: [
          {
            internalType: "string",
            name: "",
            type: "string"
          }
        ],
        stateMutability: "view",
        type: "function",
        constant: true
      }
    ],
    wallet
  );

  const nonce: BigNumber = await tokenContract.nonces(wallet.address);
  const tokenName: string = await tokenContract.name();

  const eRC20PermitEip712SignaturePayload = {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "chainId", type: "uint256" },
        { name: "verifyingContract", type: "address" },
      ],
      Permit: [
        { name: "owner", type: "address" },
        { name: "spender", type: "address" },
        { name: "value", type: "uint256" },
        { name: "nonce", type: "uint256" },
        { name: "deadline", type: "uint256" },
      ],
    },
    domain: {
      name: tokenName,
      version: "1",
      chainId: chainId,
      verifyingContract: tokenAddress,
    },
    message: {
      owner: wallet.address,
      spender: tokenTransferProxyAddress,
      value: approvalAmount.toString(),
      nonce: nonce.toNumber(),
      deadline: dayjs().add(2, "hour").unix(),
    },
    primaryType: "Permit",
  };
  

  const approveProxySignature = signTypedData({
    privateKey: bufferPrivateKey,
    data: eRC20PermitEip712SignaturePayload,
    version: SignTypedDataVersion.V4,
  });

  const apiPayload = {
    owner: wallet.address,
    spender: tokenTransferProxyAddress,
    tokenAddress,
    value: approvalAmount.toString(),
    signature: approveProxySignature,
  };

  const response = await fetch(`https://api.sx.bet/orders/approve`, {
    method: "POST",
    body: JSON.stringify(apiPayload),
    headers: { "Content-Type": "application/json" },
  });
}
```

> The above command returns json structured like this where `hash` is the transaction hash of the approve transaction. A null value of `hash` means the taker address already has an allowance set for the token of the amount specified in `value`.

```json
{
  "status": "success",
  "data": {
    "hash": "0x840763ae29b7a6adfa0e315afa47be30cdebd5b793d179dc07dc8fc4f0034965"
  }
}
```

This endpoint approves the specified `value` to be spent by `spender` on behalf of `owner` for token transfers that occur as part of the [Filling orders v2](#filling-orders-v2) flow according to Ethereum's [EIP-2612](https://eips.ethereum.org/EIPS/eip-2612) Permit Extension.  Note that `deadline` field here is only used during signature verification and that the `value` set will be the spender's allowance until changed or revoked. 

### HTTP Request

`POST https://api.sx.bet/orders/approve`

### Request payload parameters

| Name                | Required | Type                    | Description                                                                                                                                                                                                                                                 |
| ------------------- | -------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| owner              | true     | string                  | Address of the taker granting approval to TokenTransferProxy for filling orders on their behalf                                                                                                                                                           |
| spender             | true     | string                  | The address of the account which will be able to spend token amounts on behalf of the owner. In this case, the spender should be TokenTransferProxy address                                                                                                                                                             |
| tokenAddress            | true     | string                  | The token address to grant approval for                                                                                                                                             |
| value              | true     | string                  | The token amount to grant approval for, in Ethereum units                                                                                                                                                       |
| dealdine                | true     | string                  | The deadline as a UNIX timestamp format used in signature verification                                                                                                                                                        |
| signature            | true     | string                  | The generated EIP712 signature on the payload. See the example of how to compute this.                                                                                                                                                                 |

## Filling orders v2

<aside class="notice">
Coming soon! This endpoint will be available for use soon, please follow our Discord #api-changes channel to stay up to date.
</aside>

```shell
curl --location --request POST 'https://api.sx.bet/orders/fill/v2' \
--header 'Content-Type: application/json' \
--data-raw '{"taker":"0xa3bBFaB3645B2Dd4296cADc451d74574CD47Ba1a","baseToken":"0x6629Ce1Cf35Cc1329ebB4F63202F3f197b3F050B","isTakerBettingOutcomeOne":true,"stakeWei":"50000","desiredOdds":"83000000000000000000","oddsSlippage":5,"takerSig":"0x09d2603a8c8646221d6972b04a5cdd8b13d6326a267329825567a25a5e63606b07b97c84640bfb3ee4a5053083ce178d9e0c9cbdf1b1dfd519fda0594fae30dc1c","fillSalt":"69231297238279245345865414293427982207908612843136003245427437324972455931243"}'
```

```javascript
import { signTypedData, SignTypedDataVersion } from "@metamask/eth-sig-util";
import {
  BigNumber,
  constants,
  Contract,
  providers,
  utils,
  Wallet,
} from "ethers";
import { randomBytes } from "ethers/lib/utils";
import dayjs from "dayjs";

async function fillOrder() {
  const privateKey = process.env.PRIVATE_KEY;
  const takerAddress = process.env.TAKER_ADDRESS;

  // get the following from https://api.sx.bet/metadata
  const tokenTransferProxyAddress = process.env.TOKEN_TRANSFER_PROXY_ADDRESS;
  const EIP712FillHasherAddress = process.env.EIP712_FILL_HASHER_ADDRESS;
  const chainId = process.env.CHAIN_ID; // 4162 in production
  const domainVersion = process.env.DOMAIN_VERSION;

  const bufferPrivateKey = Buffer.from(privateKey!.substring(2), "hex");
  const wallet = new Wallet(privateKey).connect(
    new providers.JsonRpcProvider(process.env.RPC_URL) // find this under the 'references' section
  );
  const stakeWei = "50000"; // 50 USDC
  const marketHash = "0x0246b760b06009ece42d08e706563de1967e7f1b4799d0f559244e3f80bbc496"; // Liverpool vs Arsenal
  const baseToken = "0x6629Ce1Cf35Cc1329ebB4F63202F3f197b3F050B"; // USDC
  const desiredOdds = "83000000000000000000"; // ~1.20 decimal odds
  const oddsSlippage = 5; // 5% slippage, so worst decimal odds ~1.14
  const isTakerBettingOutcomeOne = true // taker is betting that team 1 wins
  const fillSalt = BigNumber.from(randomBytes(32)).toString();

  const signingPayload = {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "chainId", type: "uint256" },
        { name: "verifyingContract", type: "address" },
      ],
      Details: [
        { name: "action", type: "string" },
        { name: "market", type: "string" },
        { name: "betting", type: "string" },
        { name: "stake", type: "string" },
        { name: "worstOdds", type: "string" },
        { name: "worstReturning", type: "string" },
        { name: "fills", type: "FillObject" },
      ],
      FillObject: [
        { name: "stakeWei", type: "string" },
        { name: "marketHash", type: "string" },
        { name: "baseToken", type: "string" },
        { name: "desiredOdds", type: "string" },
        { name: "oddsSlippage", type: "uint256" },
        { name: "isTakerBettingOutcomeOne", type: "bool" },
        { name: "fillSalt", type: "uint256" },
        { name: "beneficiary", type: "address" },
        { name: "beneficiaryType", type: "uint8" },
        { name: "cashOutTarget", type: "bytes32" },
      ],
    },
    primaryType: "Details",
    domain: {
      name: "SX Bet",
      "6.0",
      chainId,
      EIP712FillHasherAddress,
    },
    message: {
      action: "N/A",
      betting: "N/A",
      stake: "N/A",
      worstOdds: "N/A",
      worstReturning: "N/A",
      market: marketHash
      fills: {
        stakeWei,
        marketHash,
        baseToken,
        desiredOdds,
        oddsSlippage,
        isTakerBettingOutcomeOne,
        fillSalt,
        beneficiary: constants.AddressZero,
        beneficiaryType: 0,
        cashOutTarget: constants.HashZero,
      },
    },
  };

  const signature = signTypedData({
    privateKey: bufferPrivateKey,
    data: signingPayload,
    version: SignTypedDataVersion.V4,
  });

  const apiPayload = {
    market: marketHash,
    baseToken,
    isTakerBettingOutcomeOne,
    stakeWei,
    desiredOdds,
    oddsSlippage,
    taker: takerAddress,
    takerSig: signature,
    fillSalt,
  };

  const response = await fetch(`https://api.sx.bet/orders/fill/v2`, {
    method: "POST",
    body: JSON.stringify(apiPayload),
    headers: { "Content-Type": "application/json" },
  });
}
```

> The above command returns json structured like this

```json
{
  "status": "success",
  "data": {
    "fillHash": "0x840763ae29b7a6adfa0e315afa47be30cdebd5b793d179dc07dc8fc4f0034965",
    "isPartialFill": false,
    "totalFilled": "50000",
    "averageOdds": "73000000000000000000" 
  }
}
```

This endpoint fills orders on the exchange based on the specified desiredOdds and oddsSlippage. Unlike the legacy [Filling orders v1](#filling-orders-v1) which considers orderHashes and takerAmounts based on an initial call to fetch orders, order matching is done internally <i>after</i> the built-in betting delay, optimizing the taker experience particularly during in-play betting. Furthermore, if any new orders with better odds are added during the betting delay window, those orders will be filled. Lastly, if there isn't sufficient size to support the full stake amount, taker fills will be partially filled so they can carry out a subsequent fill.

See below for the betting delays by sport which are added to guard against toxic flow and high spikes in latency from the bookmaker's side. It is effectively protection for the bookmaker. As order matching is done after the betting delay, errors observed in the past due to order cancellations within the betting delay will now be avoided.

**PREGAME**

| Sport                | Delay ( in seconds ) |
| -------------------- | -------------------- |
| Default (all sports) | 0.5                  |

**LIVE**

| Sport               | Delay ( in seconds ) |
| ------------------- | -------------------- |
| Baseball            | 12                   |
| Football            | 10                   |
| Tennis              | 10                   |
| Soccer              | 10                   |
| Basketball          | 8                    |
| Hockey              | 8                    |
| Default (all other) | 8                    |

To fill orders on sx.bet via the API, make sure you first enable betting by following the steps [here](#enabling-betting)

<aside class="notice">
Your assets must be on SX Network to place bets.
</aside>

### HTTP Request

`POST https://api.sx.bet/orders/fill/v2`

### Request payload parameters

| Name                | Required | Type                    | Description                                                                                                                                                                                                                                                 |
| ------------------- | -------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| market              | true     | string                  | User facing string for what market the user is betting on. Can simply set to "N/A" when using the API                                                                                                                                                       |
| baseToken              | true     | string                 | The address of the ERC-20 token representing the currency of the fill  |
| isTakerBettingOutcomeOne              | true     | boolean                 | Whether or not taker is betting outcome 1 (team 1 wins), if false then taker is betting outcome 2 (team 2 wins) |
| stakeWei              | true     | string                  | The stake amount for this bet in wei units - see [Unit Conversion](#unit-conversion) |
| desiredOdds                | true     | string                  | The best odds for filling, used as an anchor when applying oddsSlippage - note that any odds better than the desiredOdds can still fill if found at the time of order matching                 |
| oddsSlippage                | true     | integer                  | An integer between 0-100 representing the percentage of tolerance that is acceptable based on desiredOdds |
| fillSalt            | true     | string                  | Random 32 byte string to identify this fill. Must be the same `fillSalt` used when computing the EIP712 payload                                                                                                                                             |
| taker               | true     | string                  | Address of the taker taking the bet                                                                                                                                                                                                                         |
| takerSig            | true     | string                  | The EIP712 signature of the `taker` on the payload. See the example of how to compute this.                                                                                                                                                                 |
| message             | true     | string                  | A user-facing message for the eip712 signing. Can be anything.                                                                                                                                                                                              |
### Response format

| Name       | Type   | Description                                            |
| ---------- | ------ | ------------------------------------------------------ |
| status     | string | `success` or `failure` if the request succeeded or not |
| data       | object | The response data                                      |
| fillHash | string | A unique identifier for this fill.                     |
| isPartialFill | boolean | Whether or not the entire stake was satisfied by this fill         |
| totalFilled | string | The total amount filled (in wei), useful for determining how much to fill for subsequent bet |
| averageOdds | string | The average odds of the total amount filled          |

### Error Responses

| Error Code                 | Description                                                                  |
| ---------------------------| ---------------------------------------------------------------------------- |
| INSUFFICIENT_KYC           | The taker has not met the minimum kyc level to fill                          |
| AFTER_ORDER_EXPIRY         | One of the orders have expired                                               |
| BASE_TOKENS_NOT_SAME       | All orders must be for the same `baseToken`                                  |
| MARKETS_NOT_SAME           | All orders must be for the same market                                       |
| DIRECTIONS_NOT_SAME        | All orders must be betting on the same side `isMakerBettingOutcomeOne`       |
| INVALID_ORDERS             | Order is now inactive                                                        |
| INVALID_ODDS               | Invalid desiredOdds, must be less than 10^20                                 |
| INVALID_ODDS_SLIPPAGE      | Invalid oddsSlippage, must be an integer between 0-100                       |
| MATCH_STATE_INVALID        | The fixture for the order is in an invalid state and is not bettable anymore |
| TAKER_SIGNATURE_MISMATCH   | The taker signature generated for the request is invalid                     |
| PROXY_ACCOUNT_INVALID      | The proxy account is invalid (only applicable if proxyTaker was specified in request) |
| TAKER_AMOUNT_TOO_LOW       | The stakeWei specified is too low for the current token                      |
| META_TX_RATE_LIMIT_REACHED | Cannot have more than 10 meta transactions at once                           |
| INSUFFICIENT_SPACE         | There is not enough space to fill the matched orders due to other pending fills  |
| FILL_ALREADY_SUBMITTED     | The fill has already been submitted                                          |
| ODDS_STALE                 | No orders could not be found for the desiredOdds and oddsSlippage, try again with greater oddsSlippage |

