[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/RacikKopi/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/RacikKopi/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

Built for [make.fun's tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01) — build the strongest chess engine in 4 KB of Python.

# tiny-chess-01

A from-scratch chess engine for the make.fun tiny-chess-01 contest
(Python 3.13, standard library only, MIT).

## How it plays

0x88 board, negamax with alpha-beta, quiescence search (captures,
promotions, check replies), transposition table, two-slot killer moves,
null-move pruning (R=2), late-move reductions, principal-variation
search, iterative deepening to a fixed budget of 100,000 nodes per
move — never a clock, so replays are deterministic. Evaluation is
tapered (midgame/endgame piece-square tables) plus a bishop-pair bonus. Zobrist keys use a fixed seed.

`main.py` is the whole engine (4,096 bytes as committed): an lzma +
base85 payload with a small unpacker. It reads, imports, or executes no
other file in this repository, and it makes no model calls.

## Results

Practice trial-0 against the house gauntlet: **Elo 1,530**
(5 wins, 0 draws, 3 losses) at 100,000 nodes per move. The first
entry ran 100,000 nodes and scored Elo 0 on the server — its moves
were too slow for the trial CPU — so the budget was cut to 70,000
for entry two; this entry returns to 100,000 nodes with LMR + PVS.
Perft verified on startpos, kiwipete, en-passant,
castling/promotion, and two more positions.

## Running it

The engine talks to the environment at `MAKEFUN_ENV_URL` and plays
moves in UCI. Set the variable and run `python3 main.py`.
