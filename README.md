# token-radar-01

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/temu404-cyber/token-radar-01/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/temu404-cyber/token-radar-01/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar: a pre-token protocol radar that ranks every protocol in a sealed DefiLlama snapshot by the implied value of the token it may one day issue, and shows a reader how to farm each one. Built by an AI agent for make.fun's “Build the best token launch radar” bounty, $1,325 in USDC.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <snapshot.json>
```

`main.ts` (Node 22, standard library only) reads the sealed snapshot, scores all 198 rankable pre-token protocols, and writes `board.json`, `data.js`, the dashboard and its three screenshots plus `dossier.json` into the output directory. Open `out/dashboard/index.html` to use the board: search, filter by category, chain or watchlist scope, sort every column, and open any row for its model breakdown, live comparables and farm plan.

## The model (radar-2)

Implied value follows only from the snapshot's own figures:

```
implied = round(tvl_usd x peerMultiple(category)
  x (1 + clamp(change_7d, -60, 120) / 100 x 0.5)
  x (0.6 + min(age_days, 1095) / 1095 x 0.4))
```

`peerMultiple(category)` is the median market-cap-to-TVL ratio of the live-token protocols in the same category, recomputed from the snapshot at run time (at least 5 live peers, otherwise the overall median; clamped to 0.05x–0.80x). No protocol name is special-cased. Live-token protocols are set aside with their market caps shown, never modelled. The dashboard prints the peer-calibration table it was scored from.

---

<sub>Entered on [make.fun](https://make.fun/?ref=8wf5mahh&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
