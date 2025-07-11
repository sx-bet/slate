# Markets

## Get active markets

```shell
curl --location --request GET 'https://api.sx.bet/markets/active?onlyMainLine=true'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "markets": [
      {
        "status": "ACTIVE",
        "marketHash": "0x0d64c52e8781acdada86920a2d1e5acd6f29dcfe285cf9cae367b671dff05f7d",
        "outcomeOneName": "Nikoloz Basilashvili",
        "outcomeTwoName": "Carlos Alcaraz",
        "outcomeVoidName": "NO_CONTEST",
        "teamOneName": "Nikoloz Basilashvili",
        "teamTwoName": "Carlos Alcaraz",
        "type": 226,
        "gameTime": 1622735700,
        "sportXEventId": "L7032829",
        "liveEnabled": true,
        "sportLabel": "Tennis",
        "sportId": 6,
        "leagueId": 1070,
  ,
        "leagueLabel": "ATP French Open",
        "group1": "ATP French Open"
      },
      {
        "status": "ACTIVE",
        "marketHash": "0xe609a49d083cd41214a0db276c1ba323c4a947eefd2e4260386fec7b5d258188",
        "outcomeOneName": "Over 36.5",
        "outcomeTwoName": "Under 36.5",
        "outcomeVoidName": "NO_GAME_OR_EVEN",
        "teamOneName": "Nikoloz Basilashvili",
        "teamTwoName": "Carlos Alcaraz",
        "type": 2,
        "gameTime": 1622735700,
        "line": 36.5,
        "sportXEventId": "L7032829",
        "liveEnabled": true,
        "sportLabel": "Tennis",
        "sportId": 6,
        "leagueId": 1070,
  ,
        "leagueLabel": "ATP French Open",
        "mainLine": true,
        "group1": "ATP French Open"
      },
      {
        "status": "ACTIVE",
        "marketHash": "0x85e588d72b4a2ec6386846a6f4706dba2124410e38bd8e8f7f37dee9728e0d84",
        "outcomeOneName": "Nikoloz Basilashvili +1.5",
        "outcomeTwoName": "Carlos Alcaraz -1.5",
        "outcomeVoidName": "NO_GAME_OR_EVEN",
        "teamOneName": "Nikoloz Basilashvili",
        "teamTwoName": "Carlos Alcaraz",
        "type": 3,
        "gameTime": 1622735700,
        "line": 1.5,
        "sportXEventId": "L7032829",
        "liveEnabled": true,
        "sportLabel": "Tennis",
        "sportId": 6,
        "leagueId": 1070,
  ,
        "leagueLabel": "ATP French Open",
        "mainLine": true,
        "group1": "ATP French Open"
      }
    ],
    "nextKey": "60c7b8f54da0ad001aa3261c"
  }
}
```

This endpoint retrieves active markets on the exchange. It does not return markets that have been settled or reported. Note that to retrieve odds for a particular market, you must query the orders endpoint [the orders endpoint](#get-active-orders) separately.

### HTTP Request

`GET https://api.sx.bet/markets/active`

### Query parameters

| Name          | Required | Type     | Description                                                                                                      |
| ------------- | -------- | -------- | ---------------------------------------------------------------------------------------------------------------- |
| onlyMainLine  | false    | boolean  | If set to true, the result will only include main lines on spread and over under markets                         |
| eventId       | false    | string   | If set, it will only include markets for a particular sportXEventId                                              |
| leagueId      | false    | number   | If set, it will only include markets for a particular league ID                                                  |
| sportIds      | false    | number[] | If set, it will only include markets for particular sport IDs (comma separated)                                  |
| liveOnly      | false    | boolean  | If set, it will only include markets that are currently available for in-play betting                            |
| betGroup      | false    | string   | If set, it will only include markets for a particular bet group                                                  |
| type          | false    | number[] | If set, it will only include markets for those particular market types. See below for the options                |
| paginationKey | false    | string   | Used for pagination. Pass the `nextKey` returned from the previous request to retrieve the next set of records.  |
| pageSize      | false    | number   | Used for pagination. Requested page size. Each call will only return up to this amount of records. Maximum of 50 |

<aside class="notice">
Only one of <code>type</code> and <code>betGroup</code> can be present. Not both.
</aside>

### Response format

| Name      | Type     | Description                                                                     |
| --------- | -------- | ------------------------------------------------------------------------------- |
| status    | string   | `success` or `failure` if the request succeeded or not                          |
| data      | object   | The response data                                                               |
| > markets | Market[] | The active markets                                                              |
| > nextKey | string   | Use this key as the `paginationKey` to retrieve the next set of records, if any |

A `market` object looks like this

| Name            | Type       | Description                                                                                                                         |
| --------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| status          | string     | `ACTIVE` or `INACTIVE`                                                                                                              |
| marketHash      | string     | The unique identifier for the market                                                                                                |
| outcomeOneName  | string     | Outcome one for this market                                                                                                         |
| outcomeTwoName  | string     | Outcome two for this market                                                                                                         |
| outcomeVoidName | string     | Outcome void for this market                                                                                                        |
| teamOneName     | string     | The name of the first team/player participating                                                                                     |
| teamTwoName     | string     | The name of the second team/player participating                                                                                    |
| type            | MarketType | The type of the market                                                                                                              |
| gameTime        | number     | The UNIX timestamp of the game                                                                                                      |
| line            | number?    | The line of the market. Only applicable to markets with a line                                                                      |
| sportXEventId   | string     | The unique event ID for this market                                                                                                 |
| liveEnabled     | boolean    | Whether or not this match is available for live betting                                                                             |
| sportLabel      | string     | The name of the sport for this market                                                                                               |
| sportId         | number     | The ID of the sport for this market                                                                                                 |
| leagueId        | number     | The league ID for this market                                                                                                       |
| leagueLabel     | string     | The name of the league for this market                                                                                              |
| mainLine        | boolean?   | If this market is currently the main line or not. If the market is not a market with multiple lines, this field will not be present |
| group1          | string     | Indicator to the client of how to display this market                                                                               |
| group2          | string?    | Indicator to the client of how to display this market                                                                               |
| teamOneMeta     | string?    | Extra metadata for team one                                                                                                         |
| teamTwoMeta     | string?    | Extra metadata for team two                                                                                                         |
| marketMeta      | string?    | Extra metadata for the market overall                                                                                               |
| legs            | Market[]?  | If this is a Parlay Market, this field will contain an array of the underlying Legs as a Market object                              |

A `MarketType` can currently be one of the following

| ID   | Name                              | Has Lines | Description                                                               | Bet Group           |
| ---- | --------------------------------- | --------- | ------------------------------------------------------------------------- | ------------------- |
| 1    | 1X2                               | false     | Who will win the game (1X2)                                               | 1X2                 |
| 52   | 12                                | false     | Who will win the game                                                     | game-lines          |
| 88   | To Qualify                        | false     | Which team will qualify                                                   | game-lines          |
| 226  | 12 Including Overtime             | false     | Who will win the game including overtime (no draw)                        | game-lines          |
| 3    | Asian Handicap                    | true      | Who will win the game with handicap (no draw)                             | game-lines          |
| 201  | Asian Handicap Games              | true      | Who will win more games with handicap (no draw)                           | game-lines          |
| 342  | Asian Handicap Including Overtime | true      | Who will win the game with handicap (no draw) including Overtime          | game-lines          |
| 2    | Under/Over                        | true      | Will the score be under/over a specific line                              | game-lines          |
| 835  | Asian Under/Over                  | true      | Will the score be under/over specific asian line                          | game-lines          |
| 28   | Under/Over Including Overtime     | true      | Will the score including overtime be over/under a specific line           | game-lines          |
| 29   | Under/Over Rounds                 | true      | Will the number of rounds in the match will be under/over a specific line | game-lines          |
| 166  | Under/Over Games                  | true      | Number of games will be under/over a specific line                        | game-lines          |
| 1536 | Under/Over Maps                   | true      | Will the number of maps be under/over a specific line                     | game-lines          |
| 274  | Outright Winner                   | false     | Winner of a tournament, not a single match                                | outright-winner     |
| 202  | First Period Winner               | false     | Who will win the 1st Period Home/Away                                     | first-period-lines  |
| 203  | Second Period Winner              | false     | Who will win the 2nd Period Home/Away                                     | second-period-lines |
| 204  | Third Period Winner               | false     | Who will win the 3rd Period Home/Away                                     | third-period-lines  |
| 205  | Fourth Period Winner              | false     | Who will win the 4th Period Home/Away                                     | fourth-period-lines |
| 866  | Set Spread                        | true      | Which team/player will win more sets with handicap                        | set-betting         |
| 165  | Set Total                         | true      | Number of sets will be under/over a specific line                         | set-betting         |
| 53   | Asian Handicap Halftime           | true      | Who will win the 1st half with handicap (no draw)                         | first-half-lines    |
| 64   | Asian Handicap First Period       | true      | Who will win the 1st period with handicap (no draw)                       | first-period-lines  |
| 65   | Asian Handicap Second Period      | true      | Who will win the 2nd period with handicap (no draw)                       | second-period-lines |
| 66   | Asian Handicap Third Period       | true      | Who will win the 3rd period with handicap (no draw)                       | third-period-lines  |
| 63   | 12 Halftime                       | false     | Who will win the 1st half (no draw)                                       | first-half-lines    |
| 77   | Under/Over Halftime               | true      | Will the score in the 1st half be under/over a specific line              | first-half-lines    |
| 21   | Under/Over First Period           | true      | Will the score in the 1st period be under/over a specific line            | first-period-lines  |
| 45   | Under/Over Second Period          | true      | Will the score in the 2nd period be under/over a specific line            | second-period-lines |
| 46   | Under/Over Third Period           | true      | Will the score in the 3rd period be under/over a specific line            | third-period-lines  |
| 281  | 1st Five Innings Asian handicap   | true      | Who will win the 1st five innings with handicap (no draw)                 | first-five-innings  |
| 1618 | 1st 5 Innings Winner-12           | false     | Who will win in the 1st five innings                                      | first-five-innings  |
| 236  | 1st 5 Innings Under/Over          | true      | Will the score in the 1st five innings be under/over a specific line      | first-five-innings  |

More types will be added continuously.

## Get specific markets

```shell
curl --location --request GET 'https://api.sx.bet/markets/find'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": [
    {
      "status": "ACTIVE",
      "marketHash": "0x3cba25f2253035b015b9bb555c1bf900f6737704d57425dd2a5b60e929c33b81",
      "outcomeOneName": "Over 2.5",
      "outcomeTwoName": "Under 2.5",
      "outcomeVoidName": "NO_GAME_OR_EVEN",
      "teamOneName": "Aston Villa",
      "teamTwoName": "Burnley",
      "type": 2,
      "gameTime": 1608228000,
      "line": 2.5,
      "reportedDate": 1608234719,
      "outcome": 2,
      "teamOneScore": 0,
      "teamTwoScore": 0,
      "sportXEventId": "L6247212",
      "liveEnabled": false,
      "sportLabel": "Soccer",
      "sportId": 5,
      "leagueId": 29,
,
      "leagueLabel": "English Premier League",
      "group1": "English Premier League"
    }
  ]
}
```

This endpoint retrieves specific markets

### HTTP Request

`GET https://api.sx.bet/markets/find`

### Query parameters

| Name         | Required | Type     | Description                                                                |
| ------------ | -------- | -------- | -------------------------------------------------------------------------- |
| marketHashes | true     | string[] | The market hashes of the markets to retrieve. Comma separated. **Maximum 30.** |

### Response format

| Name   | Type     | Description                                            |
| ------ | -------- | ------------------------------------------------------ |
| status | string   | `success` or `failure` if the request succeeded or not |
| data   | Market[] | The response data                                      |

See [active markets section](#get-active-markets) for how the `Market` object is formatted. Note that there are a few additional fields if you are querying a market that has been settled/reported:

| Name         | Type   | Description                                                                                                                                                                                                                                       |
| ------------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| reportedDate | number | Time in unix seconds of when the market was reported                                                                                                                                                                                              |
| outcome      | number | The outcome of the market. Can be one of 0 1 or 2. 0 means the market was voided and stakes were returned to bettors. 1 means the outcome labeled `outcomeOneName` was the outcome. 2 means the outcome labeled `outcomeTwoName` was the outcome. |
| teamOneScore | number | Final score of team one                                                                                                                                                                                                                           |
| teamTwoScore | number | Final score of team two                                                                                                                                                                                                                           |

### Error Responses

| Error Code        | Description                                                   |
| ----------------- | ------------------------------------------------------------- |
| BAD_MARKET_HASHES | Invalid `marketHashes` or more than 30 `marketHashes` queried |

## Popular markets

```shell
curl --location --request GET 'https://api.sx.bet/markets/popular'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": [
    {
      "status": "ACTIVE",
      "marketHash": "0x66fc26c008c724d5dec2fb0bf8fb8797ecc49a4302a785cc8e5e7faf96249d8a",
      "outcomeOneName": "Ismagulov D.",
      "outcomeTwoName": "Rafael da Silva Alves",
      "outcomeVoidName": "NO_GAME",
      "teamOneName": "Ismagulov D.",
      "teamTwoName": "Rafael da Silva Alves",
      "type": 226,
      "gameTime": 1621724400,
      "sportXEventId": "L6896568",
      "liveEnabled": false,
      "sportLabel": "Mixed Martial Arts",
      "sportId": 7,
      "leagueId": 34,
,
      "leagueLabel": "UFC",
      "group1": "UFC"
    },
    {
      "status": "ACTIVE",
      "marketHash": "0xad3494f1bf10e826cd8e0faecd42e0f578f2bc9de748946fbe3d833a11764b89",
      "outcomeOneName": "West Ham United -0.5",
      "outcomeTwoName": "Southampton +0.5",
      "outcomeVoidName": "NO_GAME_OR_EVEN",
      "teamOneName": "West Ham United",
      "teamTwoName": "Southampton",
      "type": 3,
      "gameTime": 1621782000,
      "line": -0.5,
      "sportXEventId": "L6973172",
      "liveEnabled": false,
      "sportLabel": "Soccer",
      "sportId": 5,
      "leagueId": 29,
,
      "leagueLabel": "English Premier League",
      "mainLine": true,
      "group1": "English Premier League"
    }
  ]
}
```

This endpoint retrieves the top 10 popular markets by volume.

### HTTP Request

`GET https://api.sx.bet/markets/popular`

### Response format

| Name   | Type     | Description                                            |
| ------ | -------- | ------------------------------------------------------ |
| status | string   | `success` or `failure` if the request succeeded or not |
| data   | Market[] | The response data                                      |

See [active markets section](#get-active-markets) for how the `Market` object is formatted
