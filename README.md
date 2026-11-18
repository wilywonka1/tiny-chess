# tiny-chess-01 — a 4 KB chess engine

An original chess engine in a single `main.py` (4,008 bytes as committed).
The file is a compact loader: it decompresses an LZMA-packed copy of the
engine source (kept readable in the build workspace) and runs it.

The engine itself:

- 0x88 board, Zobrist hashing, make/unmake move generation (perft-verified)
- Negamax search: PVS, null-move pruning, late-move reductions, check
  extensions, transposition table, MVV-LVA, killer and history ordering
- Quiescence search over captures and promotions, with check evasions
- Tapered evaluation: material + formula piece-square tables, passed
  pawns, king endgame activity
- Fully deterministic: fixed node budgets only — no clock, no randomness
  in move choice; repetition scored against the game's real history

It plays the gauntlet through the env at `MAKEFUN_ENV_URL`, spending a
node bank across each game so late endgame moves keep a useful budget.
