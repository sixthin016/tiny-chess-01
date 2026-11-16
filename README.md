# tiny-chess-01 — 4 KB chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/sixthin016/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/sixthin016/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 0x88 alpha-beta chess engine in a single Python file (`main.py`,
4,091 bytes, stdlib only). It plays the make.fun tiny-chess-01 house
gauntlet over HTTP (`MAKEFUN_ENV_URL`).

- Negamax + alpha-beta, transposition table (persists across moves),
  killer moves, MVV-LVA capture ordering
- Quiescence search (captures; all evasions when in check)
- Iterative deepening to a fixed node budget (60,000 nodes/move —
  never a clock, so trials replay deterministically)
- Eval: material + formula piece-square tables + tapered king
  (middlegame/endgame by non-pawn material) + bishop pair +30

## Files

- `main.py` — the entry (compressed with `makefun compress`).
  This is the whole engine; it reads no other repo file.
- `engine.py` — the readable source (kept uncommitted in the folder
  so the bundle ships it beside the sessions).

## Local verification

- Perft: startpos, kiwipete, and 4 tactical positions match
  python-chess to depth 4 (20/20 checks).
- Practice trial (kit env server, 6 games vs rungs 1–6):
  **3 wins / 0 draws / 3 losses** — beats depth-2, depth-3 and
  depth-4; loses to nodes-100k/250k/500k. Estimated Elo ≈ 1,280
  (practice floor 1,154; sunfish-4k baseline ≈ 1,325–1,365).
- Speed: ~10–17k nodes/s; ~3.5 s/move at the 60k node budget,
  well under the 10 s/move limit.

## Build

```sh
node ../tiny-chess-01-kit/cli/makefun.mjs compress engine.py --out main.py
```

Run `compress` as its own command after the last source change.

---

<sub>Entered on [make.fun](https://make.fun/?ref=wffmhs5a&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
