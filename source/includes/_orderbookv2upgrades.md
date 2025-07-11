# Order Book V2 Upgrades

## How we currently fill orders

Our current endpoint used for taker order filling (see [Filling orders v1](#filling-orders-v1)) requires orderHashes and takerAmounts to be precomputed by upstream logic prior to calling the endpoint. Since this derivation of the orders and amounts are done prior to the built-in betting delay, users may have observed ODDS_STALE errors by the time the delay passed since those orders might no longer be active. This is particularly problematic during live games where the betting delay can be 8-12s long.

## What's changing

After reviewing a lot of community feedback, we've decided to implement a significant improvement in the way orders and order amounts are derived for a taker fill. Now, takers can specify their desired odds and a tolerance level associated with those odds (similar to how web3 users might select a slippage when swapping within a DEX). Orders will then be matched based on the best odds available after the betting delay. See [Filling orders v2](#filling-orders-v2) for more information on how to sign and call this new endpoint.

In addition to the new way to fill orders, we've also bundled in several other changes:

- Additional query params for [Get orders](#get-active-orders)
- New [Approve order fill](#approve-order-fill) endpoint which separates the token approval logic from the [Filling orders v2](#filling-orders-v2) flow.
- New [Get best odds](#get-best-odds) endpoint to view best available odds for a particular market or token
- New orderbook-related channels which are now sent as JSON and now include pendingFillAmounts (see [Active order updates v2](#active-order-updates-v2) and [Order book updates v2](#order-book-updates-v2))

## Breaking changes

To reduce impact as much as possible, we plan to continue to serve the fill v1 endpoint, [Filling orders v1](#filling-orders-v1) for the foreseeable future however you can find the tentative deprecation dates for breaking changes below which will also be announced on our Discord well ahead of time. 

| Change(s)                                                                        | Date           |
| ------------------------------------------------------------------------------- | -------------- |
| Deprecate `/orders/cancel` endpoint as all makers have now been using `/orders/cancel/v2` for some time now  | July 1, 2025 |
| Deprecate `active_orders` and `order_book` realtime channels as users will now be using `active_orders_v2` and `order_book_v2`  | September 1, 2025  |
