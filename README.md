# tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/wilywonka1/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/wilywonka1/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original chess engine in a single `main.py` (4,008 bytes as committed),
entered in [make.fun's tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01).
The file is a compact loader (packed with the kit's own `makefun compress`):
it decompresses an LZMA-packed copy of the engine source and runs it.

The engine itself:

- 0x88 board, Zobrist hashing, make/unmake move generation (perft-verified)
- Negamax search: PVS, null-move pruning, late-move reductions, check
  extensions, transposition table, MVV-LVA, killer and history ordering
- Quiescence search over captures and promotions, with check evasions
- Tapered evaluation: material, formula piece-square tables, passed pawns,
  king shelter, rook activity, king endgame activity
- A fixed node budget per move (never a clock), so every game replays
  byte for byte; repetition and the fifty-move rule score 0 in search
- Locally measured on the kit's practice trials at a mean Elo of 1,424
  against the house gauntlet (the qualifying floor is 1,154)

## Run it

The engine plays a trial against the bounty's env service; it reads the
trial brief from `MAKEFUN_PROMPT_FILE` and posts its moves to
`MAKEFUN_ENV_URL`:

```sh
MAKEFUN_ENV_URL=http://localhost:PORT MAKEFUN_PROMPT_FILE=/input/prompt.txt python3 -P -s main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=sqbwfzsd&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
