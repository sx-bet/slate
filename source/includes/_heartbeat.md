# Heartbeat

A user may register a `heartbeat` to SX Bet API using the Heartbeat service. An [API Key](#api-key) is necessary for this service. Once you register a heartbeat with the desired timeout value, all your open orders will be automatically cancelled if another heartbeat request is not sent within that timeout period.

This will ensure that when loss of connectivity occurs between your service and SX Bet API, there will be no exposure left on the orderbook.
## Register heartbeat

To register and refresh your heartbeat with 0 > `timeoutSeconds` <= 3600. Ping this endpoint to maintain your heartbeat after initial registration.

```shell
curl --location --request POST 'https://api.sx.bet/heartbeat' \
--header 'Content-Type: application/json' \
--header 'X-Api-Key: <YOUR-API-KEY>' \
--data-raw '{
    "requestor": "<YOUR-ACCOUNT-ADDRESS>",
    "timeoutSeconds": 10
}'
```
> The above command returns JSON structured like this

```json
{
    "status": "success",
    "data": {
        "requestor": "<YOUR-ACCOUNT-ADDRESS>",
        "timeoutSeconds": 10,
        "expiresAt": "2024-11-12T14:35:06.614Z"
    }
}
```
## Cancel heartbeat

To cancel a registered heartbeat, you may use the same request to register a heartbeat but use `timeoutSeconds=0`. This will deactivate the heartbeat and **orders will NOT be cancelled automatically**.

```shell
curl --location --request POST 'https://api.sx.bet/heartbeat' \
--header 'Content-Type: application/json' \
--header 'X-Api-Key: <YOUR-API-KEY>' \
--data-raw '{
    "requestor": "<YOUR-ACCOUNT-ADDRESS>",
    "timeoutSeconds": 0
}'
```
> The above command returns JSON structured like this

```json
{
    "status": "success",
    "data": {
        "requestor": "<YOUR-ACCOUNT-ADDRESS>",
        "timeoutSeconds": 0,
        "expiresAt": "2024-11-12T14:35:06.614Z"
    }
}
```
### HTTP Request

`POST https://api.sx.bet/heartbeat`

### Request payload parameters

| Name           | Required | Type   | Description                                                                           |
| -------------- | -------- | ------ | ------------------------------------------------------------------------------------- |
| requestor      | true     | string | The ethereum address associated with your account                                     |
| timeoutSeconds | true     | number | The number of seconds before heartbeat service times out and cancels your open orders |

<aside class="notice">
The <code>timeoutSeconds</code> value can be betwteen 0 - 3600 seconds inclusive. 
</aside>

### Response format

| Name             | Type   | Description                                                                           |
| ---------------- | ------ | ------------------------------------------------------------------------------------- |
| status           | string | `success` or `failure` if the request succeeded or not                                |
| data             | object | The response data                                                                     |
| > requestor      | string | The ethereum address associated with your account                                     |
| > timeoutSeconds | number | The number of seconds before heartbeat service times out and cancels your open orders |
| > expiresAt      | Date   | A JS Date object describing when the heartbeat will timeout/expire (UTC)              |
