# Trades

## Get active trades

```shell
curl --location --request GET 'https://api.sx.bet/trades'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "trades": [
      {
        "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
        "bettor": "0x63a4491dC73245E181c47BAe0ae9d6627E56dE55",
        "stake": "10236134166947574099",
        "odds": "50583446830801460000",
        "orderHash": "0xb47329db2a3f612748094f415f9bf478cbed2f196548ec68154bd1fc543a6f09",
        "marketHash": "0x3fd03af14bf11264f5274ed4c8cc283e4479d29d33e17409e8e7d9b26ca9f030",
        "maker": true,
        "betTime": 1607708054,
        "settled": true,
        "settleValue": 1,
        "bettingOutcomeOne": false,
        "fillHash": "0xbe846c92bec584c4d2215df76ac7d53ebab25f81a30cca5811fb93f35e8b5321",
        "tradeStatus": "SUCCESS",
        "valid": true,
        "marketHasRefunds": false,
        "outcome": 1,
        "settleDate": "2020-12-11T20:17:45.990Z"
      },
      {
        "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
        "bettor": "0x683bcf3ecc5A6e2E99ff83f3300515a584108391",
        "stake": "9999999999999999999",
        "odds": "49416553169198540000",
        "orderHash": "0xb47329db2a3f612748094f415f9bf478cbed2f196548ec68154bd1fc543a6f09",
        "marketHash": "0x3fd03af14bf11264f5274ed4c8cc283e4479d29d33e17409e8e7d9b26ca9f030",
        "maker": false,
        "betTime": 1607708054,
        "settled": true,
        "settleValue": 1,
        "bettingOutcomeOne": true,
        "fillHash": "0xbe846c92bec584c4d2215df76ac7d53ebab25f81a30cca5811fb93f35e8b5321",
        "tradeStatus": "SUCCESS",
        "valid": true,
        "marketHasRefunds": false,
        "outcome": 1,
        "settleDate": "2020-12-11T20:17:45.990Z"
      },
      {
        "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
        "bettor": "0xE965292B97CD666e85FaB99e2732b1A71046cf3F",
        "stake": "17592800276256254757",
        "odds": "69184587813620070000",
        "orderHash": "0x1534133364d8b18d803a9419914bb89a651de5e9fa1845868d6844a6670c4762",
        "marketHash": "0xcb8285aeef17d824b76cf4a00ba5f2bf256048114937c85609897e7b8967e9ca",
        "maker": true,
        "betTime": 1607719092,
        "settled": true,
        "settleValue": 1,
        "bettingOutcomeOne": true,
        "fillHash": "0xc0240cf27c111d843bc4cf2de0521ab097223de933125857343e7a6fba469172",
        "tradeStatus": "SUCCESS",
        "valid": true,
        "marketHasRefunds": false,
        "outcome": 1,
        "settleDate": "2020-12-11T22:02:19.484Z"
      },
      {
        "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
        "bettor": "0x5aC843EecBf67669d4003aa49aE5e0136dc73365",
        "stake": "7835984995472770999",
        "odds": "30815412186379930000",
        "orderHash": "0x1534133364d8b18d803a9419914bb89a651de5e9fa1845868d6844a6670c4762",
        "marketHash": "0xcb8285aeef17d824b76cf4a00ba5f2bf256048114937c85609897e7b8967e9ca",
        "maker": false,
        "betTime": 1607719092,
        "settled": true,
        "settleValue": 1,
        "bettingOutcomeOne": false,
        "fillHash": "0xc0240cf27c111d843bc4cf2de0521ab097223de933125857343e7a6fba469172",
        "tradeStatus": "SUCCESS",
        "valid": true,
        "marketHasRefunds": false,
        "outcome": 1,
        "settleDate": "2020-12-11T22:02:19.484Z"
      }
    ],
    "nextKey": "60e4b70dc476a37a5b1b15ae",
    "pageSize": 4
  }
}
```

This endpoint retrieves past trades on the exchange split up by order. This is a paginated endpoint. For example, if a trade fills more than one order at once, it will show up as two entries for the bettor.

### HTTP Request

`GET https://api.sx.bet/trades`

### Query parameters

| Name          | Required | Type     | Description                                                                                                     |
| ------------- | -------- | -------- | --------------------------------------------------------------------------------------------------------------- |
| startDate     | false    | number   | Only get trades placed after this time in UNIX seconds                                                          |
| endDate       | false    | number   | Only get trades placed before this time in UNIX seconds                                                         |
| bettor        | false    | string   | Only get trades placed by this bettor (regardless if maker or taker)                                            |
| settled       | false    | boolean  | If `true`, only get settled trades                                                                              |
| marketHashes  | false    | string[] | Only get trades for particular markets. Comma separated                                                         |
| baseToken     | false    | string   | Only get trades placed for a particular token                                                                   |
| maker         | false    | boolean  | If `true`, only get trades where the bettor is the maker                                                        |
| affiliate     | false    | string   | Only get trades under this affiliate                                                                            |
| pageSize      | false    | number   | Requested page size. Each call will only return up to this amount of records. Default is 100.                   |
| paginationKey | false    | string   | Used for pagination. Pass the `nextKey` returned from the previous request to retrieve the next set of records. |
| tradeStatus   | false    | string   | Filter trades to see only those with `SUCCESS` or `FAILED` status'                                              |
### Response format

| Name       | Type    | Description                                                                       |
| ---------- | ------- | --------------------------------------------------------------------------------- |
| status     | string  | `success` or `failure` if the request succeeded or not                            |
| data       | object  | The response data                                                                 |
| > trades   | Trade[] | The trades for the request                                                        |
| > nextKey  | string  | Use this key as the `paginationKey` to retrieve the next set of records, if any   |
| > pageSize | number  | Maximum amount of records on this page. Will be equal to the `pageSize` passed in |

<aside class="notice">
Fields marked with an '*' are coming soon in future release.
</aside>

A `Trade` object has the following format

| Name                     | Type    | Description                                                                                                                          |
| ------------------------ | ------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| baseToken                | string  | The token in which this trade was placed                                                                                             |
| bettor                   | string  | The address of the bettor who placed the trade                                                                                       |
| stake                    | string  | Exact token amount that was staked for the bet. To convert into a readable token amount, see [the token conversion section](#tokens) |
| normalizedStake	         | string  | The `stake` value in the correct decimal format for the `baseToken`                                                                  |
| odds                     | string  | Implied odds that the bettor received for this bet. Divide by 10^20 to get the odds in decimal format.                               |
| orderHash                | string  | The unique identifier of the order that was filled for this trade                                                                    |
| marketHash               | string  | The unique identifier of the market for which this trade was placed                                                                  |
| maker                    | boolean | `true` if the bettor is market maker in this trade                                                                                   |
| betTime                  | number  | The time in UNIX seconds when the trade was placed                                                                                   |
| settled                  | boolean | `true` if this bet is settled (this refers to if the bet was won lost or voided, not if the trade succeeded or not)                  |
| bettingOutcomeOne        | boolean | `true` if the bettor is betting outcome one in the market                                                                            |
| fillHash                 | string  | The unique identifier for this trade                                                                                                 |
| tradeStatus              | string  | `SUCCESS` or `FAILED` depending on if this trade succeeded or not                                                                    |
| valid                    | boolean | `true` if the trade counts toward competitions or tournaments                                                                        |
| marketHasRefunds*        | boolean | `true` if capital‑efficient refunds exist for this trade's market group; if `true`, query [Get portoflio refunds](#get-portfolio-refunds) for details            |
| outcome                  | number  | with `settled=true`, this will be 0, 1, or 2 depending on the final outcome of the market                                            |
| settleDate               | string  | ISO formatted date string of when the trade was settled                                                                              |
| chainVersion             | string  | `SXN` or `SXR`. See [migration docs](#sx-rollup-migration-guide).                                                                    |
| sportXeventId            | string  | The event related to this trade                                                                                                      |
| netReturn                | string  | The net return amount in the `baseToken` value                                                                                       |
| settleNetReturnValue     | string  | The net return amount in USD (at the time of settlement)                                                                             |


## Get trades by orderHash

```shell
curl --location --request GET 'https://api.sx.bet/trades/orders'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "trades": [
      {
        "baseToken": "0x6629Ce1Cf35Cc1329ebB4F63202F3f197b3F050B",
        "tradeStatus": "SUCCESS",
        "bettor": "0x5B3498Cb20C3107B5B267fabd3601B6425BDeb42",
        "stake": "907458563",
        "odds": "54750000000000000000",
        "orderHash": "0xb338c7d03b09d6cefdf2cd7e79f72ea601cfd0fa10c35b351c7a59d5c8125675",
        "marketHash": "0x526e24b9eca9bcbd51e4a19135a998e6a8d8fff06bd6668bfb8f35528837a1c2",
        "maker": true,
        "betTime": "2025-04-24T06:39:37.078Z",
        "betType": 0,
        "betTimeValue": 907.458563,
        "settled": true,
        "settleValue": 1,
        "bettingOutcomeOne": false,
        "fillHash": "0xb6b15fe7d4d337ff0ae0e2a233203385e619c5e1edf23f04135efbf12128def8",
        "affiliate": "0x0000000000000000000000000000000000000000",
        "valid": true,
        "marketHasRefunds": false,
        "providerEventId": "15468276",
        "settleDate": "2025-04-24T17:38:24.885Z",
        "outcome": 2,
        "contractsVersion": "6.0",
        "settleTxHash": "0x0b33bf455a90469bdbc30ebea3a9930fe1f1525c03895c45c8e4feb98d6ac365",
        "fillOrderHash": "0xe6f4410a4fbd649e8fc72d764056fbd01c27d8b9d2749bd2cf78f2a161dde963",
        "chainVersion": "SXR",
        "sportXeventId": "L15468276",
        "netReturn": "1657.458563",
        "settleNetReturnValue": "1657.458563",
        "normalizedStake": "907.458563"
      },
      {
        "baseToken": "0x6629Ce1Cf35Cc1329ebB4F63202F3f197b3F050B",
        "tradeStatus": "SUCCESS",
        "bettor": "0xA3C9202458BBE5EBa0b962835487d817f3955d01",
        "stake": "750000000",
        "odds": "45250000000000000000",
        "orderHash": "0xb338c7d03b09d6cefdf2cd7e79f72ea601cfd0fa10c35b351c7a59d5c8125675",
        "marketHash": "0x526e24b9eca9bcbd51e4a19135a998e6a8d8fff06bd6668bfb8f35528837a1c2",
        "maker": false,
        "betTime": "2025-04-24T06:39:37.078Z",
        "betType": 1,
        "betTimeValue": 750,
        "settled": true,
        "settleValue": 1,
        "bettingOutcomeOne": true,
        "fillHash": "0xb6b15fe7d4d337ff0ae0e2a233203385e619c5e1edf23f04135efbf12128def8",
        "affiliate": "0x0000000000000000000000000000000000000000",
        "valid": true,
        "marketHasRefunds": false,
        "providerEventId": "15468276",
        "settleDate": "2025-04-24T17:38:24.885Z",
        "outcome": 2,
        "contractsVersion": "6.0",
        "settleTxHash": "0x0b33bf455a90469bdbc30ebea3a9930fe1f1525c03895c45c8e4feb98d6ac365",
        "fillOrderHash": "0xe6f4410a4fbd649e8fc72d764056fbd01c27d8b9d2749bd2cf78f2a161dde963",
        "chainVersion": "SXR",
        "sportXeventId": "L15468276",
        "netReturn": "1657.458564",
        "settleNetReturnValue": "0",
        "normalizedStake": "750.0"
      }
    ]
  }
}
```

This endpoint retrieves trades on the exchange for the given orderHashes.

### HTTP Request

`GET https://api.sx.bet/trades/orders`

### Query parameters

| Name            | Required | Type       | Description                                                                                                     |
| --------------- | -------- | ---------- | --------------------------------------------------------------------------------------------------------------- |
| orderHashes     | true     | string[]   | The unique identifiers of the orders being searched                                                             |
### Response format

| Name       | Type    | Description                                                                       |
| ---------- | ------- | --------------------------------------------------------------------------------- |
| status     | string  | `success` or `failure` if the request succeeded or not                            |
| data       | object  | The response data                                                                 |
| > trades   | Trade[] | The trades for the request                                                        |

## Get consolidated trades

```shell
curl --location --request GET 'https://api.sx.bet/trades/consolidated'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "trades": [
      {
        "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
        "tradeStatus": "SUCCESS",
        "bettor": "0x025b9FD9F1ed818d688e19c5F43c500bf44cEA47",
        "totalStake": "4.999999999999999999",
        "weightedAverageOdds": "67564738292011016000",
        "marketHash": "0x7b27d766b6e36b87e2b7924f792c4f84d9b459318735d69cbb7d695b0857f8d5",
        "maker": false,
        "settled": false,
        "fillHash": "0xc44e72f94e70ede9742c6b8aeb77e743e0cbf753ff3eae8bd4f1ab98b9260f0e",
        "gameLabel": "Australia vs New Zealand",
        "bettingOutcomeLabel": "Australia",
        "sportXEventId": "L6350002",
        "bettingOutcome": 1,
        "gameTime": "2021-01-06T23:30:00.000Z",
        "leagueLabel": "International Test",
        "outcome": 0,
        "marketHasRefunds": false,
        "netReturn": "4.999999999999999999"
      },
      {
        "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
        "tradeStatus": "SUCCESS",
        "bettor": "0x025b9FD9F1ed818d688e19c5F43c500bf44cEA47",
        "totalStake": "4.999999999999999999",
        "weightedAverageOdds": "67564738292011016000",
        "marketHash": "0x7b27d766b6e36b87e2b7924f792c4f84d9b459318735d69cbb7d695b0857f8d5",
        "maker": false,
        "settled": false,
        "fillHash": "0xc44e72f94e70ede9742c6b8aeb77e743e0cbf753ff3eae8bd4f1ab98b9260f0e",
        "gameLabel": "Australia vs New Zealand",
        "bettingOutcomeLabel": "Australia",
        "sportXEventId": "L6350002",
        "bettingOutcome": 1,
        "gameTime": "2021-01-06T23:30:00.000Z",
        "leagueLabel": "International Test",
        "outcome": 0,
        "marketHasRefunds": false,
        "netReturn": "4.999999999999999999"
      }
    ],
    "count": 100
  }
}
```

This endpoint retrieves past consolidated trades on the exchange via pagination. If a trade fills multiple orders, it will show up as one entry here per bettor.

### HTTP Request

`GET https://api.sx.bet/trades/consolidated`

### Query parameters

| Name          | Required | Type    | Description                                                        |
| ------------- | -------- | ------- | ------------------------------------------------------------------ |
| bettor        | false    | string  | Only get trades placed by this bettor                              |
| settled       | true     | boolean | If `true` only get settled trades                                  |
| page          | true     | number  | Page number for pagination                                         |
| perPage       | true     | number  | Amount of records to fetch per page                                |
| sortBy        | true     | string  | Which field to sort by (see response for field names)              |
| sortAsc       | true     | boolean | If `true`, sorts in ascending order                                |
| maker         | false    | boolean | If `true`, only gets trades where the bettor was a market maker    |
| sportXEventId | false    | string  | Only gets trades for this event ID                                 |
| tradeStatus   | false    | string  | Filter trades to see only those with `SUCCESS` or `FAILED` status' |

### Response format

| Name     | Type                | Description                                            |
| -------- | ------------------- | ------------------------------------------------------ |
| status   | string              | `success` or `failure` if the request succeeded or not |
| data     | any                 | The response data                                      |
| > trades | ConsolidatedTrade[] | The consolidated trades for this request               |
| > count  | number              | Total count of trades for this query                   |

A `ConsolidatedTrade` object has the following format

| Name                | Type    | Description                                                                                                                                 |
| ------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| baseToken           | string  | The token in which this trade was placed                                                                                                    |
| tradeStatus         | string  | `SUCCESS` or `FAILED` depending on if this trade succeeded or not                                                                           |
| bettor              | string  | The address of the bettor who placed the trade                                                                                              |
| totalStake          | string  | Total nominal stake of the trade                                                                                                            |
| weightedAverageOdds | string  | Weighted average odds (based on stake) of the trade if the trade filled multiple orders. Divide by 10^20 to get the odds in decimal format. |
| marketHash          | string  | The unique identifier of the market for which this trade was placed                                                                         |
| maker               | boolean | `true` if the bettor is market maker in this trade                                                                                          |
| settled             | boolean | `true` if this bet is settled (this refers to if the bet was won lost or voided, not if the trade succeeded or not)                         |
| fillHash            | string  | The unique identifier for this trade                                                                                                        |
| gameLabel           | string  | A general label for the market                                                                                                              |
| bettingOutcomeLabel | string  | Which team/side the bettor bet                                                                                                              |
| sportXEventId       | string  | The unique fixture ID for this trade                                                                                                        |
| bettingOutcome      | number  | `1` if the bettor is betting outcome one, `2` otherwise                                                                                     |
| gameTime            | string  | ISO formatted date string of when the game is suppossed to occur                                                                            |
| leagueLabel         | string  | The name of this league                                                                                                                     |
| outcome             | number  | With `settled=true`, this will be 0, 1, or 2 depending on the final outcome of the market                                                   |
| chainVersion        | string  | `SXN` or `SXR`. See [migration docs](#sx-rollup-migration-guide).                                                                           |
| sportXeventId       | string  | The event related to this trade                                                                                                             |
| marketHasRefunds*   | boolean | `true` if capital efficient refunds exist for this market group; if `true`, query [Get portoflio refunds](#get-portfolio-refunds) for details                          |

## Get portfolio refunds

<aside class="notice">
Coming soon! This endpoint will be available for use soon, please follow our Discord #api-changes channel to stay up to date.
</aside>

```shell
curl --location --request GET 'https://api.sx.bet/trades/portfolio/refunds?bettor=0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F&sortAsc=false&page=0&perPage=500'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "results": [
      {
        "marketHash": "0x3e012cc2842849b96768547d4c92720d7ee8946e7706323f5114b6451708cf5e",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 2.346033,
        "events": [
          {
            "maker": false,
            "amount": "2.346033",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-21T14:29:26.805266+00:00",
            "marketHash": "0x3e012cc2842849b96768547d4c92720d7ee8946e7706323f5114b6451708cf5e",
            "fillOrderHash": "0x7efa8ee211c5cbccebda722318252ee09cfadaa9c910bf4c433086d853784b02"
          }
        ]
      },
      {
        "marketHash": "0x14081d3be87bcdc2cb81c616e9eb5a487506af4abad1b7495a66d9768d6352c2",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 2.698125,
        "events": [
          {
            "maker": false,
            "amount": "2.698125",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-21T14:27:37.892992+00:00",
            "marketHash": "0x14081d3be87bcdc2cb81c616e9eb5a487506af4abad1b7495a66d9768d6352c2",
            "fillOrderHash": "0x5a5f7ff232699f73db7c29af3631f47b1f338e3b5279bcf851ff05b63292e71c"
          }
        ]
      },
      {
        "marketHash": "0x30bb58ae1c28d04ab9e94c313eb6d9656c0854248bd0273cb13edcd8e337155a",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 3.695149,
        "events": [
          {
            "maker": false,
            "amount": "3.695149",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-21T14:26:39.85327+00:00",
            "marketHash": "0x30bb58ae1c28d04ab9e94c313eb6d9656c0854248bd0273cb13edcd8e337155a",
            "fillOrderHash": "0x179e4d8cfad8dcc16f8188dc7714a54b2bfb60335e3aba305120919c2419be9a"
          }
        ]
      },
      {
        "marketHash": "0x0760c1c1fe427ff04bec6488702637918f7daa8cae7b2411017e692caaa28e6c",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 19.559896,
        "events": [
          {
            "maker": false,
            "amount": "9.779948",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-20T15:25:15.899042+00:00",
            "marketHash": "0x0760c1c1fe427ff04bec6488702637918f7daa8cae7b2411017e692caaa28e6c",
            "fillOrderHash": "0xea2423b823246d7d12833e1834123a86ddb208f7f1eb63e06dd2d31303f37f32"
          },
          {
            "maker": false,
            "amount": "9.779948",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-20T15:25:15.730559+00:00",
            "marketHash": "0x0760c1c1fe427ff04bec6488702637918f7daa8cae7b2411017e692caaa28e6c",
            "fillOrderHash": "0xea2423b823246d7d12833e1834123a86ddb208f7f1eb63e06dd2d31303f37f32"
          }
        ]
      },
      {
        "marketHash": "0x381fba172f94f121026047e4944edcf895550dffd90627f2e76843705f1a633a",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 18.561474,
        "events": [
          {
            "maker": false,
            "amount": "9.280737",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-20T15:03:48.323011+00:00",
            "marketHash": "0x381fba172f94f121026047e4944edcf895550dffd90627f2e76843705f1a633a",
            "fillOrderHash": "0x4faa50c4e6aa5074b8305db34050e7aaf675bd6d4c32c18ac159a8122587ae61"
          },
          {
            "maker": false,
            "amount": "9.280737",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-20T15:03:48.214994+00:00",
            "marketHash": "0x381fba172f94f121026047e4944edcf895550dffd90627f2e76843705f1a633a",
            "fillOrderHash": "0x4faa50c4e6aa5074b8305db34050e7aaf675bd6d4c32c18ac159a8122587ae61"
          }
        ]
      },
      {
        "marketHash": "0xf84c30678aecadab705cd492b3b4c1b58c2589c9e8bac070b17860affa63c17f",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 13.289026,
        "events": [
          {
            "maker": false,
            "amount": "5.881642",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-17T23:22:45.667688+00:00",
            "marketHash": "0xf84c30678aecadab705cd492b3b4c1b58c2589c9e8bac070b17860affa63c17f",
            "fillOrderHash": "0x1fa325f322649c9d21086c6702bd4ce3210e32781d12ea7e54fc301796cb39bb"
          },
          {
            "maker": false,
            "amount": "7.407384",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-17T18:52:00.185707+00:00",
            "marketHash": "0xf84c30678aecadab705cd492b3b4c1b58c2589c9e8bac070b17860affa63c17f",
            "fillOrderHash": "0xa0bfe79dcf7c4488aa685cc91d02381143a5f4b505e1ccb18b33b5f4cbf8fe7f"
          }
        ]
      },
      {
        "marketHash": "0xed9963a520580046eed9675cef34d38050854a3734494e7b37ea265f548bbe37",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 6.153813,
        "events": [
          {
            "maker": false,
            "amount": "6.153813",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-16T21:26:16.143613+00:00",
            "marketHash": "0xed9963a520580046eed9675cef34d38050854a3734494e7b37ea265f548bbe37",
            "fillOrderHash": "0x8e1faaa91c6164b72de3b3a42c516e4947c111e8e05d5f59655a7ba58f7dc788"
          }
        ]
      },
      {
        "marketHash": "0x319d42ff612a1b0cbd5865690e067877f509aa943a89d3a819abba8b412d8f35",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 7.889529,
        "events": [
          {
            "maker": false,
            "amount": "7.889529",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-16T21:24:50.05795+00:00",
            "marketHash": "0x319d42ff612a1b0cbd5865690e067877f509aa943a89d3a819abba8b412d8f35",
            "fillOrderHash": "0x2403cbb53f0223ad9dec5213ab251960c6b7af427ae0b438e4c2504245eafd28"
          }
        ]
      },
      {
        "marketHash": "0x5bf33fb43e24a16ea507defabebce86f9cd481cb3d5e057aebba4f63b265a75a",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 9.367678,
        "events": [
          {
            "maker": false,
            "amount": "9.367678",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-15T19:54:46.63248+00:00",
            "marketHash": "0x5bf33fb43e24a16ea507defabebce86f9cd481cb3d5e057aebba4f63b265a75a",
            "fillOrderHash": "0xd22c09f4a888d283cb495ac1a428063a57e5182c338408aca6c563643e183077"
          }
        ]
      },
      {
        "marketHash": "0x1a5521437acd388bf31da31b655e7f38c2b5df9f72686bb0e2252a435bf57305",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 7.393698,
        "events": [
          {
            "maker": false,
            "amount": "7.393698",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-10-02T21:12:00.458343+00:00",
            "marketHash": "0x1a5521437acd388bf31da31b655e7f38c2b5df9f72686bb0e2252a435bf57305",
            "fillOrderHash": "0xcca366280794ef6e5a84275780cc7fd5dc9345613464510ee7178a08a4f1daff"
          }
        ]
      },
      {
        "marketHash": "0x3b9d3fab07560742bf8ecf7e50ef28ccbbcfb0288bead1ac599898939c1958e7",
        "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
        "totalRefunded": 17.977509,
        "events": [
          {
            "maker": false,
            "amount": "17.977509",
            "bettor": "0xaD6A65315Cb20dD0b9D0Af56213516727a20C66F",
            "baseToken": "0x1BC6326EA6aF2aB8E4b6Bc83418044B1923b2956",
            "createdAt": "2025-09-19T14:16:44.283611+00:00",
            "marketHash": "0x3b9d3fab07560742bf8ecf7e50ef28ccbbcfb0288bead1ac599898939c1958e7",
            "fillOrderHash": "0x98795dacfcb0023420e1dcb40ffba19bbc84e0df7feb6b8f1f50b423bfd57633"
          }
        ]
      }
    ],
    "count": 11
  }
}
```

This endpoint retrieves capital‑efficient refund events for a bettor, aggregated by market. It supports reconciling cases where `settledNetReturn` may differ from `netReturn` when `marketHasRefunds` is `true` (see Capital Efficiency Upgrades). Refunds reflect decreases in worst‑case exposure (MXL) from offsetting positions and are only generated for market groups without prior cash outs; conversely, cash outs cannot occur after capital‑efficient refunds.

See [Capital Efficiency Upgrade](#capital-efficiency-upgrade) for a high-level overview of the Capital Efficiency Upgrade.

### HTTP Request

`GET https://api.sx.bet/trades/portfolio/refunds`

### Query parameters

| Name          | Required | Type    | Description                                                                 |
| ------------- | -------- | ------- | --------------------------------------------------------------------------- |
| bettor        | true     | string  | Bettor address (checksummed).                                               |
| marketHash    | false    | string  | Filter by market hash.                                                      |
| baseToken     | false    | string  | Filter by base token.                                                       |
| fillOrderHash | false    | string  | Filter by the associated trade fill hash.                                   |
| maker         | false    | boolean | If `true`, only refunds where bettor was a maker; otherwise taker refunds.  |
| sortAsc       | true     | boolean | Sort ascending when `true`, descending when `false`.                        |
| page          | true     | number  | Page number for pagination (min 0).                                         |
| perPage       | true     | number  | Page size (max 500).                                                        |

### Response format

| Name         | Type              | Description                                             |
| ------------ | ----------------- | ------------------------------------------------------- |
| status       | string            | `success` or `failure`                                  |
| data         | object            | The response payload                                    |
| > results    | PortfolioRefund[] | Aggregated refunds by market                            |
| > count      | number            | Total count of aggregated market results                |

A `PortfolioRefund` object has the following format

| Name          | Type          | Description                                            |
| ------------- | ------------- | ------------------------------------------------------ |
| marketHash    | string        | Market hash for this refund aggregation                |
| baseToken     | string        | Base token of the refunds                              |
| totalRefunded | number        | Sum of refund amounts for this market in base token    |
| events        | RefundEvent[] | Individual refund events that make up the aggregation  |

A `RefundEvent` object has the following format

| Name         | Type    | Description                                   |
| ------------ | ------- | --------------------------------------------- |
| maker        | boolean | `true` if bettor was maker for this refund    |
| amount       | string  | Refund amount in base token (string‑encoded)  |
| bettor       | string  | Bettor address                                |
| baseToken    | string  | Token address                                 |
| createdAt    | string  | ISO date string of event creation             |
| marketHash   | string  | Market hash                                   |
| fillOrderHash| string  | Fill hash associated with the refund          |
