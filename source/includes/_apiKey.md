# API Key

This key is currently required to access the WebSocket through Ably, for realtime updates. Otherwise, in order to use the SX.Bet API, you do NOT need an API Key. The standard API user can perform all the requests provided in this document. There is a baseline rate limiter applied to all requests, regardless of API key.

The API Key will 

<aside class="notice">
You must obtain an API Key in order to connect to the WebSocket via Ably.
</aside>

## Generating API Key

1. Visit <a href='https://sx.bet'>sx.bet</a> and register/login to your account. You can connect your MetaMask wallet, or login using your Fortmatic email address.
2. If using MetaMask, `sign` the Signature Request.
3. Click the `Account` tab on the top navigation bar.
4. Click the `Overview` tab on the account navigation bar.
5. You will see an `API Credentials` card. Complete the `Enhanced Verification` if you have not yet done so by clicking the link in the card.
6. If you've signed in and completed the enhanced verification, you can now click the button: `GENERATE API KEY NOW`. An API Key will be displayed.
7. The API Key generated will not be displayed again, so please <b>copy and save this key for future use</b>.

<aside class="notice">
If you lose your key, you can generate a new one by following the same steps. Any previous keys used will be unauthorized if you generate a new key.
</aside>

## Usage

```shell
curl --location --request GET 'https://api.sx.bet/user/token' \
--header 'X-Api-Key: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX'
```

> You must fill your API Key in the header `X-Api-Key`. The above is a sample command to create an Ably Token Request.

Once your API Key is generated (see above), you must add it as a HTTP Header with the name: `X-Api-Key`.
