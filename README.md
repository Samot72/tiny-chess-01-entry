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
