# tiny-chess-01 — 4 KB chess engine

A compact, original chess engine in a single `main.py` (4,055 bytes),
written for the make.fun tiny-chess-01 bounty ("strongest chess engine
in 4 KB of Python").

## Design

- **Board:** 0x88 mailbox, incremental material + piece-square eval
  (tapered middlegame/endgame king tables, bishop-pair bonus, tempo).
- **Search:** iterative deepening alpha-beta to a fixed node budget
  (never a clock, so trials replay deterministically), with
  principal-variation search, null-move pruning, late-move reductions,
  transposition table, killer moves and history heuristic.
- **Quiescence:** captures and promotions, plus all replies to check.
- **Budgets:** per-game node budgets (5k vs the weakest rung up to
  60k vs the strongest), tuned so the slowest move stays well under
  the 10 s limit on 1 CPU (~1.2 s/move average in practice trials).
- **Protocol:** talks to the env at `$MAKEFUN_ENV_URL` only
  (`/game`, `/move`), plays UCI moves, no model calls, no randomness.

## Files

- `main.py` — the whole engine (MIT). It is a compressed payload with
  its unpacker (allowed by the rules); the readable source is developed
  outside this snapshot.
- `LICENSE` — MIT.

## Grade it

From the kit directory:

    node cli/makefun.mjs grade-local --kit . --bot <this repo> --driver process
