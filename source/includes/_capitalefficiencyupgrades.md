# Capital Efficiency Upgrade

## Current escrow behaviour

Currently, our escrow smart contract does not account for hedged exposure across opposing outcomes within the same market group. As a result, if a taker or maker bets $100 at +100 on Team A to win and later $100 at +100 on Team B to win, a total of $200 would be locked up in escrow until settlement, even though these positions offset. At settlement, a portion of these funds is guaranteed to be returned. 

SX's Capital Efficiency (CE) upgrade introduces logic to recognize such scenarios earlier on (during the order filling phase as opposed to upon settlement) and release appropriate amounts from escrow while keeping the orderbook fully collateralized.

## What's changing

We are introducing capital‑efficient (CE) refunds driven by a maximum‑loss (MXL) algorithm computed at the market‑group level:

- When a new trade reduces your portfolio’s worst‑case (maximum) loss for a market group, the system will issue a refund for the decrease, releasing some of the previously locked escrow. This applies to both takers and makers. Although refund transfer events are triggered by the action of a taker placing a bet, the refund computations apply to both taker and maker(s) at the time that bet is placed. 
- MXL logic calculates the worst‑case net loss across all open positions within a market group. Our Escrow contract tracks this worst‑case. Whenever MXL decreases due to offsetting exposure (e.g. hedges on opposing outcomes), refunds are generated to return the difference.

### Upcoming changes

- New API endpoint: [Get portoflio refunds](#get-portfolio-refunds)
  - Query by `bettor`, `marketHash`, `baseToken`, and `fillOrderHash` to retrieve capital-efficient refunds associated with a specific trade or market.
  - Use this endpoint to reconcile why realized or settled net return values may differ from expected values as a result of CE refunds that may have occurred.
- New `marketHasRefunds` boolean on Trade and ConsolidatedTrade API reponse objects
  - Present on [Get active trades](#get-active-trades), [Get trades by orderHash](#get-trades-by-orderhash) and [Get consolidated trades](#get-consolidated-trades) responses. 
  - If `true`, users can query [Get portoflio refunds](#get-portfolio-refunds) to reference the refund records for the associated `marketHash`/`baseToken`/`fillOrderHash`. This helps explain cases where `settledNetReturn` does not match the expected `netReturn`, as the `settledNetReturn` takes any prior refund amounts into consideration.
- Realtime publishing
  - Related trade and consolidated trade realtime publishes include the `marketHasRefunds` flag to make it known to clients that the market group is associated with one or more refunds.
  - A [CE refund events](#ce-refund-events) channel publishes refund events for consumers who want to ingest refund updates as they happen.

## CE Refunds vs. Taker Cash Out

- Refunds can only occur within market groups that have no bets that have already been cashed out.
- Conversely, cash outs cannot occur for any markets that have already received CE refunds.

This mutual exclusivity prevents double counting risk release and ensures consistent accounting.

## Breaking changes

- New `marketHasRefunds` boolean field is included on Trade and ConslidatedTrade objects within [Get active trades](#get-active-trades), [Get trades by orderHash](#get-trades-by-orderhash), and [Get consolidated trades](#get-consolidated-trades) API responses and is published in related realtime messages.

