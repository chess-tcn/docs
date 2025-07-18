# Python API Reference
All functions in the `chess_tcn` module.

---
## decode_tcn
```python
decode_tcn(tcn: str) -> list[dict]
```

Decodes a TCN‐encoded string into a list of move dictionaries.

**Parameters:**
- `tcn` (str) – raw TCN data from Chess.com or similar sources.

**Returns:**
- `list[dict]` – a list of moves where each dict may include:
  - `"from"` (str) – origin square (absent on drop moves)
  - `"to"` (str) – destination square
  - `"promotion"` (str) – promoted piece (`"q"|"r"|"n"|"b"|"k"|"p"`)
  - `"drop"` (str) – dropped piece (`"q"|"r"|"n"|"b"|"k"|"p"`)

**Example:**
```python
moves = decode_tcn("mC0Kgv7Tbq5Qlt9IqHT7cM1TMFWOHs2MFwZRfm6Eeg")
print(moves)
# [
#     {'from': 'e2', 'to': 'e4'},
#     {'from': 'e7', 'to': 'e5'},
#     ...
# ]
```

---
## encode_tcn
```python
encode_tcn(moves: list[dict] | dict) -> str
```

Serializes one or more move dictionaries into a TCN‐encoded string.

**Parameters:**
- `moves` (dict | list[dict]) – a single move dict or a list of them (same shape as returned by `decode_tcn`).

**Returns:**
- `str` – the TCN representation of the provided moves.

**Example:**
```python
moves = [
    {'from': 'e2', 'to': 'e4'},
    {'from': 'e7', 'to': 'e5'}
]
tcn = encode_tcn(moves)
print(tcn)  # mC0K
```

---
## tcn_to_pgn
```python
tcn_to_pgn(tcn: str) -> str
```

Plays a sequence of TCN moves on a fresh `python-chess` board and returns standard SAN‐numbered PGN.

**Parameters:**
- `tcn` (str) – raw TCN move list.

**Returns:**
- `str` – PGN move-text (e.g. `"1. e4 e5 2. Nf3 Nc6 ..."`).

**Raises:**
- `ValueError` if any decoded move is illegal.

**Example:**
```python
pgn = tcn_to_pgn("mC0Kgv7Tbq5Qlt9IqHT7cM1TMFWOHs2MFwZRfm6Eeg")
print(pgn)  # "1. e4 e5 2. Nf3 Nc6 ..."
```

---
## pgn_to_tcn
```python
pgn_to_tcn(pgn: str) -> str
```

Loads PGN move-text into `python-chess`, extracts its mainline moves, and encodes them into TCN.

**Parameters:**
- `pgn` (str) – valid PGN move-text.

**Returns:**
- `str` – the TCN‐encoded representation of the game.

**Raises:**
- `ValueError` if the PGN fails to parse or is invalid.

**Example:**
```python
tcn = pgn_to_tcn("1. e4 e5 2. Nf3 Nc6")
print(tcn) # mC0Kgv5Q
```
