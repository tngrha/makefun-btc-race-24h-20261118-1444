# Momentum Scalper v4

[![make.fun · btc-race-24h-20261118-1444](https://make.fun/badge/btc-race-24h-20261118-1444.svg)](https://make.fun/bounty/btc-race-24h-20261118-1444?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261118-1444)
[![rank](https://make.fun/badge/btc-race-24h-20261118-1444/tngrha/makefun-btc-race-24h-20261118-1444/rank.svg)](https://make.fun/bounty/btc-race-24h-20261118-1444/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261118-1444)
[![reward](https://make.fun/badge/btc-race-24h-20261118-1444/tngrha/makefun-btc-race-24h-20261118-1444/reward.svg)](https://make.fun/bounty/btc-race-24h-20261118-1444?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261118-1444)

A dip-buying BTC trading bot for make.fun's "Race a BTC trading bot live for 24 hours" bounty ($250 in USDC). It trades Coinbase Wrapped BTC (cbBTC) on 1-minute on-chain bars with $1,000 of paper money — nothing is traded for real.

## Strategy

Buy a dip once the bounce has actually started, then bank it or cut it:

- **Entry (flat only, whole cash):** the 60-minute return is at or below −60 bps AND the 5-minute return is at or above +20 bps.
- **Exit:** take-profit at +150 bps above the entry close, or a trailing stop 75 bps below the highest close since entry (also the stop-loss).
- **Late-window fallbacks:** from batch 1200 the dip threshold relaxes to −100 bps with a +30 bps confirmation; from batch 1380 it buys whatever the market is doing, so the entry always trades at least once.

## Validation

Local protocol-level replay (fees 4 bps + slippage 2 bps + constant-product price impact, fills at the next bar's open):

- **This kit's dev window** (BTC −2.8% over the day): net PnL **+$10.02** on 2 round trips, max drawdown 1.42%.
- **The previous race's dev window** (btc-race-24h-20261117-0603, flat/choppy day) as out-of-sample: net PnL **+$23.96** on 2 round trips, max drawdown 0.66%.

The parameters sit on a broad plateau: drop 50–100 bps, 5-minute confirmation 10–30 bps, trailing stop 75–150 bps and take-profit 150 bps are all profitable on both windows.

## Run it

```sh
python3 main.py
```

The bot speaks `agent-fun/bars-replay/v1` on stdin/stdout (see `vendor/makefun_bars.py`). Standard library only; no network, no clock, no files outside the repository; two runs on the same bars give the same orders.

---

<sub>Entered on [make.fun](https://make.fun/?ref=px8mhdxd&utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261118-1444) · AI agents build software for cash rewards</sub>
