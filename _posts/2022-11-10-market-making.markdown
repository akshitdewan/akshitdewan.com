---
layout: post
title:  "Market Making"
date:   2022-11-09 23:51:01 -0800
permalink: mm.html
---
I tried to find a good description of market making online, but the articles I found seemed to each be missing components or a complete example [^1]. So I'm going to give it a go!
<!-- This post won't attempt to cover all parts of market making, only offer a complete and self contained example. -->

I'll start with an example scenario on the stock market, and then provide connections to things you may have seen in markets.

#### Example: trading AAPL shares

This example is self contained, and you can skip the rest of the post while still understanding market making! 

Let's say we have a market for AAPL. The lowest asking seller, Alice, wants to sell her share at $10. The highest bidding buyer, Bob, wants to buy a share at $5. While those two are fighting it over, John decides he wants to sell one of his shares, soon. His best option is to sell to Bob at $5. Later, Janice arrives and wants to buy a share, also soon. Her best option is to buy it at $10 from Alice.

```
$10: Alice sells, Janice buys
      -
      -
      -
      -
$5: Bob buys, John sells
``` 

Something wasn't optimal there. If Janice had just arrived a little bit earlier, her and John could have traded with each other and gotten a better deal. For example, if they traded at $7.5, they would both be better off by $2.5. But sadly, they weren't around at the same time.

```
$10: Alice wants to sell 
      -
      -
$7.5: John sells, Janice buys
      -
      -
$5: Bob wants to buy
``` 

Let's start the example again, including Alice and Bob's dear friend Citadel in the mix. Alice and Bob are again offering $10 and $5 to sell and buy respectively. Citadel says: I'll buy AAPL from anyone at $6.5 and sell it at $8.5. John shows up to sell his share and he takes Citadel's $6.5 offer. Janice arrives later and buys a share, buying from citadel for $8.5, which is cheaper than Alice. In this scenario, John and Janice both got a better deal.

```
$10: Alice wants to sell 
      -
$8.5: Citadel sells, Janice buys
      -
$6.5  John sells, Citadel buys
      -
$5: Bob wants to buy
``` 

So what happened here? Citadel was willing to hold John's share temporarily until Janice arrived. This allowed them both to get a better price than before. John and Janice had no guarantee that the other would arrive, so Citadel was rewarded with $2 for taking the risk.

#### Risk
Why does the market maker get to profit? Time.

In the example before, the market maker profited because of the delay between John and Janice's arrival. They were willing to bet that Janice would show up eventually and hold the goods till then. In the general setting, the market maker also has to worry about the price of AAPL changing. If the market maker owns apple shares, then the price of AAPL going down means they won't profit. If they owe apple shares (e.g. are short AAPL), the price of AAPL going up will cause them a loss.

#### Spreads
The market maker can choose to put the bid and ask anywhere, as long as they put the bid higher than the ask. In our example, the market maker gave a $6.5 to $8.5 range. This gap of $2 is the market maker's profit and is known as a spread.

In practice, this range is much smaller, often closer to a few cents per spread. This is because many market makers are competing to get the sale. If there was only one market maker, they could get away with charging just a little bit below the ask price and offering close to the bid price. Then, the consumers would barely benefit but the market maker would have the most profit.

Spreads are affected by things like market maker operational costs and risk. If a market maker has few costs, they can afford to set narrower spreads. If the markets are highly volatile, a market maker might want to set a wider spread, to compensate for the additional risk.


#### Displayed Price

How is a single price displayed for stocks if there is a spread between the bid and ask? Typically, the displayed price is actually the last price at which a transaction happened. This price does NOT have to correspond with the price you pay--you will always pay the asking price.


#### Simpler real world example
We can see this idea in examples outside of the stock market, too. One of the functions of a retail store is to market make by buying a specific amount of a product and betting on being able to sell it later. For example, Best Buy could buy 500 Wii's from Nintendo, so Nintendo can sell profit immediately. Consumers can then show up at any time to buy the Wii from Best Buy, but Nintendo didn't have to wait for consumers to show up!

[^1]: The examples I found all seemed to be missing the time component of market making. They'd say that a market maker advertises a bid and ask, and profits by selling at the ask and buying at the bid while keeping the ask higher than the bid. I'd always be left asking, "If there is a buyer willing to pay the ask price and another willing to pay the bid price, why wouldn't they just trade for each other and save some money?". The answer is that these two buyers don't exist at the same time.