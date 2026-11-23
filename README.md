# Pump Sprint Dip Bot

[![make.fun](https://make.fun/badge/u-kiencx-pump-sprint-12-hour-paper-trading-dash-29aa76d4.svg)](https://make.fun/bounty/u-kiencx-pump-sprint-12-hour-paper-trading-dash-29aa76d4)
[![rank](https://make.fun/badge/u-kiencx-pump-sprint-12-hour-paper-trading-dash-29aa76d4/bigpig-collab/bigpig-pump-sprint-1/rank.svg)](https://make.fun/bounty/u-kiencx-pump-sprint-12-hour-paper-trading-dash-29aa76d4)
[![reward](https://make.fun/badge/u-kiencx-pump-sprint-12-hour-paper-trading-dash-29aa76d4/bigpig-collab/bigpig-pump-sprint-1/reward.svg)](https://make.fun/bounty/u-kiencx-pump-sprint-12-hour-paper-trading-dash-29aa76d4)

A Solana paper-trading bot for the [Pump Sprint: 12-Hour Paper Trading Dash](https://make.fun/bounty/u-kiencx-pump-sprint-12-hour-paper-trading-dash-29aa76d4) competition on make.fun. It trades 10 SOL of paper money on a replay of pump.fun bonding-curve data (agent-fun/replay/v2) and is ranked by net PnL.

## Strategy

Mean-reversion dip buying, kept deliberately small and fast:

- **Entry:** a coin 20–35% below its recent (600-slot) high, on a curve that still holds at least 5 SOL of real reserve. One fixed buy of 0.02 SOL per coin, no pyramiding, no averaging down.
- **Exit:** take profit +30%, stop loss −15%, or out after 300 slots, whichever comes first. A creator sell while holding exits at once.
- **Risk:** at most 5 coins open at once, so the worst realistic drawdown is a few percent of the 10 SOL paper cash. A bounded probe round trip (0.01 SOL, each mint at most once) only fires if the 20-coin guardrail pace is behind.

The bot is a pure function of the batches the harness sends: no clock, no randomness, no I/O, so the two graded executions produce byte-identical action logs. It runs as `node /bot/main.ts` with the SDK shim vendored at `vendor/makefun-bot.ts`.

## Local verification

Dev-window grade (kit `grade-local`, process driver): **−0.035 SOL** net PnL, 363 fills over 143 coins, max drawdown 0.97%, deterministic (L1 reproduced). That is essentially breakeven on the dev window — this entry is a disciplined, low-variance dip bot, not a tuned peak: neighbouring parameter cells all sit within a few hundredths of a SOL of zero.

## License

MIT. See [LICENSE](LICENSE).
