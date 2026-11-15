# tiny-chess-01 — a chess engine in under 4 KB of Python

`main.py` is the whole engine: a negamax alpha-beta search with iterative
deepening to a fixed node budget (40,000 nodes a move — no clock, no
randomness, so every replay plays the same moves). Inside: quiescence search
(captures and promotions, all evasions when in check), a transposition table,
PVS, null-move pruning, late move reductions, MVV-LVA / killer move ordering,
and an incremental material + piece-square evaluation with a bishop-pair
bonus and an endgame king table. It plays the make.fun house gauntlet through
the env at `MAKEFUN_ENV_URL` (POST /game, /move).

The file is lzma-packed (the rules allow a compressed payload with its
unpacker inside the 4,096-byte cap); the unpacked source is the engine's
code, written for this competition. MIT licensed — see LICENSE.

## Verification (local, before submission)

Move generation is perft-exact on the standard suites: start position
20 / 400 / 8,902; Kiwipete 48 / 2,039; the en-passant-pin position
14 / 191 / 2,812; the promotion position 6 / 264. The packed file is
4,074 bytes; the whole repository snapshot is 6,028 bytes. Measured on a
shared VM the engine runs at roughly 38,000–41,000 nodes/s, so the slowest
move at the 40,000-node cap takes about 1.1 s — well inside the 10 s move
limit, with the trial's 1,800 s wall in mind. It finds mate-in-1 (Qxf7#)
and plays the gauntlet through the real practice env from the kit.
