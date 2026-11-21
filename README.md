# tiny-chess-4k

A chess engine in 4 KB of Python, built for the
[make.fun tiny-chess-01 bounty](https://make.fun/c/tiny-chess-01).

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/FiluFafayo/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/FiluFafayo/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

## Engine

`main.py` is the whole engine (LZMA-packed, unpacks at runtime — packing
is allowed by the competition rules). Inside:

- 0x88 board, full legal move generation (castling, en passant, promotions)
- Negamax alpha-beta with iterative deepening to a fixed node budget
  (22,000 nodes/move — deterministic, no clock, so replays match)
- Quiescence search over captures, promotions and replies to check
- Transposition table, killer moves, MVV-LVA capture ordering
- Evaluation: material + piece-square tables + bishop-pair bonus

It plays the house gauntlet through the env at `MAKEFUN_ENV_URL`
(`POST /game`, `POST /move`), one game after another, and exits when the
trial is done.

## Local check

Perft verified against python-chess on the start position, Kiwipete,
and en-passant/promotion positions. Graded locally against the kit's
practice trial-0 env (see the submission report for the score).
