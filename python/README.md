# Chess TCN Python

A Python library for encoding and decoding TCN, a move format used by **Chess.com**'s API.

## Installation

```bash
pip install chess-tcn
```

## Quick Start

```python
from chess_tcn import decode_tcn, encode_tcn, tcn_to_pgn, pgn_to_tcn

# Example TCN string (e.g. from Chess.com live‐game API)
tcn_string = "mC0Kgv7Tbq5Qlt9IqHT7cM1TMFWOHs2MFwZRfm6Eeg"

# Decode TCN to a list of move dicts
moves = decode_tcn(tcn_string)
print("Decoded moves (dicts):", moves)

# Re-encode that move list back into a TCN string
reencoded_tcn = encode_tcn(moves)
print("Re-encoded TCN string:", reencoded_tcn)

# Convert the TCN string directly to a PGN move-text string
pgn_text = tcn_to_pgn(tcn_string)
print("PGN move-text:", pgn_text)

# Convert a PGN move-text string back into TCN
roundtrip_tcn = pgn_to_tcn(pgn_text)
print("TCN from PGN:", roundtrip_tcn)
```

## API Reference

See [API.md](API.md) for full details.
