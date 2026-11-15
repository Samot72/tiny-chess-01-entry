[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Samot72/tiny-chess-01-entry/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Samot72/tiny-chess-01-entry/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01 — a chess engine in under 4 KB of Python

`main.py` is the whole engine (v2): a negamax alpha-beta search with
iterative deepening to a fixed node budget (75,000 nodes a move — no clock,
no randomness, so every replay plays the same moves). Inside: quiescence
search (captures and promotions, all evasions when in check), a Zobrist
transposition table, PVS, null-move pruning, late move reductions, and move
ordering by TT move, MVV-LVA captures, killers and a gravity history
heuristic. The board is 0x88 with piece lists; evaluation is incremental
material + piece-square tables. It plays the make.fun house gauntlet
through the env at `MAKEFUN_ENV_URL` (POST /game, /move).

The file is lzma-packed (the rules allow a compressed payload with its
unpacker inside the 4,096-byte cap); the unpacked source is the engine's
code, written for this competition. MIT licensed — see LICENSE.

## Verification (local, before submission)

Move generation is perft-exact on the standard suites: start position
20 / 400 / 8,902; Kiwipete 48 / 2,039 / 97,862; the en-passant-pin position
14 / 191 / 2,812; the promotion position 6 / 264 / 9,467; make/unmake state
restoration is checked exactly over random playouts. The packed file is
3,331 bytes; the whole repository snapshot is 6,546 bytes. On the kit's
three practice instances it scores 1,451 / 1,451 / 1,809 (mean 1,570),
against 1,279 / 1,279 / 1,099 (mean 1,219) for the v1 entry. It finds
mate-in-1 (Qxf7#) and plays the gauntlet through the real practice env
from the kit.
