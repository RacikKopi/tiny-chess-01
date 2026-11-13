# tiny-chess-01

A from-scratch chess engine for the make.fun tiny-chess-01 contest
(Python 3.13, standard library only, MIT).

## How it plays

0x88 board, negamax with alpha-beta, quiescence search (captures,
promotions, check replies), transposition table, two-slot killer moves,
null-move pruning (R=2), and iterative deepening to a fixed budget of
100,000 nodes per move — never a clock, so replays are deterministic.
Evaluation is tapered (midgame/endgame piece-square tables) plus a
bishop-pair bonus. Zobrist keys use a fixed seed.

`main.py` is the whole engine (4,009 bytes as committed): an lzma +
base85 payload with a small unpacker. It reads, imports, or executes no
other file in this repository, and it makes no model calls.

## Results

Practice trial-0 against the house gauntlet: **Elo 1,464**
(4 wins, 1 draw, 3 losses). Perft verified on startpos, kiwipete,
en-passant, castling/promotion, and two more positions.

## Running it

The engine talks to the environment at `MAKEFUN_ENV_URL` and plays
moves in UCI. Set the variable and run `python3 main.py`.
