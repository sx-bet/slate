# Orders

## Get active orders

```shell
curl --location --request POST 'https://app.api.sportx.bet/orders'
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
      "expiry": 1631233201,
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
      "expiry": 1631233201,
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
      "expiry": 1631233201,
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

`POST https://app.api.sportx.bet/orders`

### Request payload parameters

| Name         | Required | Type     | Description                                    |
| ------------ | -------- | -------- | ---------------------------------------------- |
| marketHashes | false    | string[] | Only get orders for these market hashes        |
| baseToken    | false    | string   | Only get orders denominated in this base token |
| maker        | false    | string   | Only get orders for this market maker          |

Note that one of `marketHashes` or `maker` is required.

### Response format

| Name                     | Type    | Description                                                                                                                                                                                                                                                                                                                                    |
| ------------------------ | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fillAmount               | string  | How much this order has been filled in Ethereum units up to a max of `totalBetSize`. See [the token section](#tokens) of how to convert this into nominal amounts                                                                                                                                                                              |
| orderHash                | string  | A unique identifier for this order                                                                                                                                                                                                                                                                                                             |
| marketHash               | string  | The market corresponding to this order                                                                                                                                                                                                                                                                                                         |
| maker                    | string  | The market maker for this order                                                                                                                                                                                                                                                                                                                |
| totalBetSize             | string  | The total size of this order in Ethereum units. See the [the token section](#tokens) section for how to convert this into nominal amounts.                                                                                                                                                                                                     |
| percentageOdds           | string  | The odds that the `maker` receives in the sportx protocol format. To convert to an implied odds divide by 10^20. To convert to the odds that the taker would receive if this order would be filled in implied format, use the formula `takerOdds=1-percentageOdds/10^20`. See the [unit conversion section](#bookmaker-odds) for more details. |
| expiry                   | number  | The time in unix seconds after which this order is no longer valid                                                                                                                                                                                                                                                                             |
| baseToken                | string  | The base token this order is denominated in                                                                                                                                                                                                                                                                                                    |
| executor                 | string  | The address permitted to execute on this order. This is set to the sportx.bet exchange                                                                                                                                                                                                                                                         |
| salt                     | string  | A random number to differentiate identical orders                                                                                                                                                                                                                                                                                              |
| isMakerBettingOutcomeOne | boolean | `true` if the maker is betting outcome one (and hence taker is betting outcome two if filled)                                                                                                                                                                                                                                                  |
| signature                | string  | Signature of the maker on this order                                                                                                                                                                                                                                                                                                           |

<aside class="notice">
Note that <code>totalBetSize</code> and <code>fillAmount</code> are from *the perspective of the market maker*. <code>totalBetSize</code> can be thought of as the maximum amount of tokens the maker will be putting into the pot if the order was fully filled. <code>fillAmount</code> can be thought of as how many tokens the maker has already put into the pot. To compute how much space there is left from the taker's perspective, you can use the formula <code>remainingTakerSpace = (totalBetSize - fillAmount) * 10^20 / percentageOdds - (totalBetSize - fillAmount)</code>
</aside>

## Enabling betting

```shell
See the javascript section.
```

```javascript
import { MaxUint256 } from "ethers/constants";
import { Contract } from "ethers";
import { JsonRpcProvider } from "ethers/providers";

// You can get an RPC url from https://docs.matic.network/docs/develop/network-details/network/

const walletAddress = process.env.WALLET_ADDRESS;
const tokenAddress = process.env.TOKEN_ADDRESS;
const tokenTransferProxyAddress = process.env.TOKEN_TRANSFER_PROXY_ADDRESS;
const provider = new providers.JsonRpcProvider(process.env.POLYGON_RPC_URL);
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
await tokenContract.approve(tokenTransferProxyAddress, MaxUInt256);
```

To enable betting, you need to approve the `TokenTransferProxy` contract for each token for which you wish to trade. Otherwise, any endpoints that create/cancel or fill orders will fail. For example if you want to trade with both ETH and USDC, you'll need to approve the contract twice, once for each token. The address of the `TokenTransferProxy` is `0xa6EA1Ed4aeC85dF277fae3512f8a6cbb40c1Fe7e` and the address of each token is given in [the tokens section](#tokens)

If you don't wish to do this programmatically, you can simply go to `https://sportx.bet`, make a test bet with the account and token you'll be using, and you will be good to go.

If you want to do it programmatically, see the code sample on the right. Note you will need a little bit of MATIC to make this transaction (~$0.01 worth).

## Post a new order

```shell
curl --location --request POST 'https://app.api.sportx.bet/orders/new' \
--header 'Content-Type: application/json' \
--data-raw '{
    "orders": [
        {
            "marketHash": "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
            "maker": "0x6F75bA6c90E3da79b7ACAfc0fb9cf3968aa4ee39",
            "totalBetSize": "21600000000000000000",
            "percentageOdds": "47846889952153115000",
            "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
            "expiry": "1631233201",
            "executor": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
            "isMakerBettingOutcomeOne": true,
            "signature": "0x50b00e7994b0656f78701537296444bccba2a7e4d46a84ff26c8ca48cb66774c76faa893be293412959779900232065c8236e489158070777d7a3e1a37d911811b",
            "salt": "61882422358902283358380622686147595792242782952753619716150366288606659190035"
        }
    ]
}'
```

```javascript
import { BigNumber, utils, providers, Wallet } from "ethers";

const order = {
  marketHash:
    "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
  maker: "0x6F75bA6c90E3da79b7ACAfc0fb9cf3968aa4ee39",
  totalBetSize: BigNumber.from("21600000000000000000"),
  percentageOdds: BigNumber.from("47846889952153115000"),
  baseToken: "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
  expiry: BigNumber.from(1631233201),
  executor: "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
  isMakerBettingOutcomeOne: true,
  salt: BigNumber.from(utils.randomBytes(32)),
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

const result = await fetch("https://app.api.sportx.bet/orders/new", {
  method: "POST",
  body: JSON.stringify({ orders: [signedOrder] }),
  headers: { "Content-Type": "application/json" },
});
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

This endpoint offers new orders on the exchange (market making).

To offer bets on sportx.bet via the API, make sure you first enable betting by following the steps [here](#enabling-betting).

### HTTP Request

`POST https://app.api.sportx.bet/orders/new`

### Request payload parameters

| Name   | Required | Type             | Description            |
| ------ | -------- | ---------------- | ---------------------- |
| orders | true     | SignedNewOrder[] | The new orders to post |

A `SignedNewOrder` object looks like this

| Name                     | Type    | Description                                                                                              |
| ------------------------ | ------- | -------------------------------------------------------------------------------------------------------- |
| marketHash               | string  | The market you wish to place this order under                                                            |
| maker                    | string  | The ethereum address offering the bet                                                                    |
| baseToken                | string  | The token this order is denominated in                                                                   |
| totalBetSize             | string  | The total bet size of the order in Ethereum units.                                                       |
| percentageOdds           | string  | The odds _the maker will be receiving_ as this order gets filled                                         |
| expiry                   | number  | Time in UNIX seconds after which this order is no longer valid                                           |
| executor                 | string  | The sportx.bet executor address. See the [metadata section](#get-metadata) for where to get this address |
| salt                     | string  | A random 32 byte string to differentiate between between orders with otherwise identical parameters      |
| isMakerBettingOutcomeOne | boolean | `true` if the maker is betting outcome one (and hence taker is betting outcome two if filled)            |
| signature                | string  | The signature of the maker on this order payload                                                         |

### Response format

| Name     | Type     | Description                                            |
| -------- | -------- | ------------------------------------------------------ |
| status   | string   | `success` or `failure` if the request succeeded or not |
| data     | object   | The response data                                      |
| > orders | string[] | The order hashes corresponding to the new orders       |

<aside class="notice">
Note that <code>totalBetSize</code> is from *the perspective of the market maker*. <code>totalBetSize</code> can be thought of as the maximum amount of tokens the maker (you) will be putting into the pot if the order was fully filled. This is the maximum amount you will risk.
</aside>

## Cancel orders

```shell
curl --location --request POST 'https://app.api.sportx.bet/orders/cancel' \
--header 'Content-Type: application/json' \
--data-raw '{"message":"Are you sure you want to cancel these orders?","orders":["0x4ead6ef92741cd0b6e1ea32cb1d9586a85165e8bd780ab6f897992428c357bf1"],"cancelSignature":"0x1fe66a4ed7fbd2cf9e918f5b6b73db4f46166f871f7c0f293080ee07d63592ef0d29cd0aa37dc68e25a9d483515cc3ceb4934baaed8f0114385f8c43f28677aa1c"}'
```

```javascript
import ethSigUtil from "eth-sig-util";

// Example is shown using a private key

const privateKey = process.env.PRIVATE_KEY;
const bufferPrivateKey = Buffer.from(privateKey.substring(2), "hex");
const ordersToCancel = [
  "0x4ead6ef92741cd0b6e1ea32cb1d9586a85165e8bd780ab6f897992428c357bf1",
];

const payload = {
  types: {
    EIP712Domain: [
      { name: "name", type: "string" },
      { name: "version", type: "string" },
      { name: "chainId", type: "uint256" },
    ],
    Details: [
      { name: "message", type: "string" },
      { name: "orders", type: "string[]" },
    ],
  },
  primaryType: "Details",
  domain: {
    name: "CancelOrderSportX",
    version: "1.0",
    chainId: 1,
  },
  message: {
    message: "Are you sure you want to cancel these orders",
    orders: ordersToCancel,
  },
};

const signature = ethSigUtil.signTypedData_v4(bufferPrivateKey, {
  data: payload,
});

const payload = {
  orders: ordersToCancel,
  message: "Are you sure you want to cancel these orders",
  signature,
};

const result = await fetch("https://app.api.sportx.bet/orders/cancel", {
  method: "POST",
  body: JSON.stringify(payload),
  headers: { "Content-Type": "application/json" },
});
```

> The above command returns json structured like this

```json
{
  "status": "success",
  "data": {
    "orderHashes": [
      "0x4ead6ef92741cd0b6e1ea32cb1d9586a85165e8bd780ab6f897992428c357bf1"
    ]
  }
}
```

This endpoint cancels existing orders on the exchange.

### HTTP Request

`POST https://app.api.sportx.bet/orders/cancel`

### Request payload parameters

| Name      | Required | Type     | Description                                                                                                                                            |
| --------- | -------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| orders    | true     | string[] | The order hashes to cancel                                                                                                                             |
| message   | true     | string   | A user-facing message for the eip712 signing. Can be anything.                                                                                         |
| signature | true     | string   | The EIP712 signature on the cancel order payload. See the [EIP712 signing section](#eip712-signing) for more details on how to compute this signature. |

### Response format

| Name          | Type     | Description                                            |
| ------------- | -------- | ------------------------------------------------------ |
| status        | string   | `success` or `failure` if the request succeeded or not |
| data          | object   | The response data                                      |
| > orderHashes | string[] | The cancelled order hashes                             |

## Filling orders

```shell
curl --location --request POST 'https://app.api.sportx.bet/orders/fill' \
--header 'Content-Type: application/json' \
--data-raw '{"orderHashes":["0x863a2288a640e1bb722da2ee7a6f323ea28caee8ac681d320534d0e7f2e849de","0x001f676d68baf85310145f85bc5aeba64108b234607b4fae25c704069ca8464a"],"takerAmounts":["10000000000000000000","10000000000000000000"],"taker":"0xa3bBFaB3645B2Dd4296cADc451d74574CD47Ba1a","takerSig":"0x09d2603a8c8646221d6972b04a5cdd8b13d6326a267329825567a25a5e63606b07b97c84640bfb3ee4a5053083ce178d9e0c9cbdf1b1dfd519fda0594fae30dc1c","fillSalt":"69231297238279245345865414293427982207908612843136003245427437324972455931243","action":"N/A","market":"N/A","betting":"N/A","stake":"N/A","odds":"N/A","returning":"N/A"}'
```

```javascript
import ethSigUtil from "eth-sig-util";
import {
  BigNumber,
  constants,
  Contract,
  providers,
  utils,
  Wallet,
} from "ethers";
import { randomBytes } from "ethers/lib/utils";

async function fillOrder() {
  const privateKey = process.env.PRIVATE_KEY;
  const takerAddress = process.env.TAKER_ADDRESS;
  const tokenAddress = process.env.TOKEN_ADDRESS;
  const tokenTransferProxyAddress = process.env.TOKEN_TRANSFER_PROXY_ADDRESS;
  const bufferPrivateKey = Buffer.from(privateKey!.substring(2), "hex");
  const wallet = new Wallet(privateKey).connect(
    new providers.JsonRpcProvider(process.env.PROVIDER_URL)
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
            name: "user",
            type: "address",
          },
        ],
        name: "getNonce",
        outputs: [
          {
            internalType: "uint256",
            name: "nonce",
            type: "uint256",
          },
        ],
        stateMutability: "view",
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
    ],
    wallet
  );

  let nonce: BigNumber;
  if (
    tokenAddress === "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174" // USDC has a non-standard get nonce method
  ) {
    nonce = await tokenContract.nonces(takerAddress);
  } else {
    nonce = await tokenContract.getNonce(takerAddress);
  }
  const tokenName: string = await tokenContract.name();
  const abiEncodedFunctionSig = tokenContract.interface.encodeFunctionData(
    "approve",
    [tokenTransferProxyAddress, approvalAmount]
  );

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
      expiry: 1631233201,
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
      expiry: 1631233201,
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
      name: "SportX",
      version: "1.0",
      chainId: 1,
      verifyingContract: "0xCc4fBba7D0E0F2A03113F42f5D3aE80d9B2aD55d",
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
      },
    },
  };

  const approveProxySigningPayload = {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "verifyingContract", type: "address" },
        { name: "salt", type: "bytes32" },
      ],
      MetaTransaction: [
        { name: "nonce", type: "uint256" },
        { name: "from", type: "address" },
        { name: "functionSignature", type: "bytes" },
      ],
    },
    domain: {
      name: tokenName,
      version: "1",
      salt: utils.hexZeroPad(utils.hexlify(137), 32),
      verifyingContract: tokenAddress,
    },
    message: {
      nonce,
      from: takerAddress,
      functionSignature: abiEncodedFunctionSig,
    },
    primaryType: "MetaTransaction",
  };

  const approveProxySignature = ethSigUtil.signTypedData_v4(bufferPrivateKey, {
    data: approveProxySigningPayload,
  });

  const signature = ethSigUtil.signTypedData_v4(bufferPrivateKey, {
    data: signingPayload,
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

  const response = await fetch(`https://app.api.sportx.bet/orders/fill`, {
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

Note that pre-game has a built-in betting delay of 2s and in-game betting has a built-in betting delay of 5s. This is added to guard against toxic flow and high spikes in latency from the bookmaker's side. It is effectively protection for the bookmaker. If the odds change within that delay time, the order will be cancelled and an error will be thrown.

To fill orders on sportx.bet via the API, make sure you first enable betting by following the steps [here](#enabling-betting)

### HTTP Request

`POST https://app.api.sportx.bet/orders/fill`

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
| stake               | true     | string                  | User facing string for how much the user is risking. Can simly set to "N/A" when using the API.                                                                                                                                                             |
| takerAmounts        | true     | string[]                | How much each order is being filled, ordered by index. Must be in the same order as `orderHashes`, and the same length as `orderHashes`. It also must be the same and in the same order as the `takerAmounts` array used when computing the EIP712 payload. |
| takerSig            | true     | string                  | The EIP712 signature on the payload. See the example of how to compute this.                                                                                                                                                                                |
| message             | true     | string                  | A user-facing message for the eip712 signing. Can be anything.                                                                                                                                                                                              |
| signature           | true     | string                  | The EIP712 signature on the cancel order payload. See the [EIP712 signing section](#eip712-signing) for general information on how to compute this signature. See the example for the specific parameters required.                                         |
| approveProxyPayload | false    | `ApproveSpenderPayload` | Extra object required if you wish to atomically `ERC20.approve()` prior to the bet. This can be useful from a UX point of view if you don't want the user to have to wait until the approval is mined before the bet can be submitted                       |

where an `ApproveSpenderPayload` looks like

| Name         | Required | Type   | Description                                                                                                                                                                                      |
| ------------ | -------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| owner        | true     | string | Address of the bettor                                                                                                                                                                            |
| spender      | true     | string | Address of the contract permitted to spend tokens on behalf of the bettor to bet. See the `TokenTransferProxy` address in the [contract-addresses](#contract-addresses) section for this address |
| tokenAddress | true     | string | Address of the token being used to bet. Must be the same as the token referenced in the orders being filled                                                                                      |
| amount       | true     | string | Amount of tokens to approve. Must be greater than or equal to the total tokens bet from the bettors's perspective, i.e., how many tokens are leaving the bettor's wallet                         |
| signature    | true     | string | The EIP712 signature of the this payload.                                                                                                                                                        |

### Response format

| Name       | Type   | Description                                            |
| ---------- | ------ | ------------------------------------------------------ |
| status     | string | `success` or `failure` if the request succeeded or not |
| data       | object | The response data                                      |
| > fillHash | string | A unique identifier for this fill.                     |

<aside class="warning">
Note that <code>fillAmounts</code> are from *the perspective of the market maker*. <code>fillAmounts</code> can be thought of as how many tokens the maker(s) will be putting into the pot. Given an amount you as the taker want to bet, you can use the following formula to convert what value you have to use as <code>fillAmount</code> in this endpoint. <code>fillAmount = takerBetAmount * percentageOdds / (10^20 - percentageOdds)</code>
</aside>

<aside class="notice">
To convert a <code>fillAmount</code> (what the market maker pays) to what the taker will pay, you can use the formula <code>takerPayAmount = fillAmount * 10^20 / percentageOdds - fillAmount </code>. Intuitively, this is the pot size (<code>fillAmount * 10^20 / percentageOdds)</code> minus what the maker is putting in
</aside>