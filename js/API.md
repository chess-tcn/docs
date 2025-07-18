# JavaScript API Reference
All exported functions in the `chess-tcn` package.

---
## decodeTCN
```js
decodeTCN(tcnString: string): Move[]
```

Converts a TCN-encoded string into an array of move objects.

**Parameters:**
- `tcnString` (string) – raw TCN data from Chess.com or similar sources.

**Returns**:
- `Move[]` – list of moves with the following shape:
  - `from?: string` – origin square (e.g. `"e2"`). Omitted on drop moves.  
  - `to: string` – destination square (e.g. `"e4"`).  
  - `promotion?: "q"|"r"|"n"|"b"|"k"|"p"` – piece promoted to.  
  - `drop?: "q"|"r"|"n"|"b"|"k"|"p"` – piece dropped (for variants allowing drops).

**Example:**
```js
const moves = decodeTCN("mC0Kgv7Tbq5Qlt9IqHT7cM1TMFWOHs2MFwZRfm6Eeg");
console.log(moves);
/*
[
    { from: "e2", to: "e4" },
    { from: "e7", to: "e5" },
    ...
]
*/
```

---
## encodeTCN
```js
encodeTCN(moves: Move | Move[]): string
```

Serializes one or more move objects into a TCN-encoded string.

**Parameters:**
- `moves` (Move | Move[]) – a single move or an array of moves as returned by `decodeTCN` or constructed manually.

**Returns:**
- `string` – the TCN representation of the provided moves.

**Example:**
```js
const tcnString = encodeTCN([
    { from: "e2", to: "e4" },
    { from: "e7", to: "e5" }
]);
console.log(tcnString); // mC0K
```

---
## tcnToPgn
```js
tcnToPgn(tcnString: string): string
```

Plays a sequence of TCN moves on a fresh Chess.js board and returns standard SAN-numbered PGN.

**Parameters:**
- `tcnString` (string) – raw TCN move list.

**Returns:**
- `string` – PGN move text (e.g. `"1. e4 e5 2. Nf3 Nc6"`).

**Throws:**
- `Error` if any decoded move is illegal.

**Example:**
```js
const pgn = tcnToPgn("mC0Kgv7Tbq5Qlt9IqHT7cM1TMFWOHs2MFwZRfm6Eeg");
console.log(pgn); // "1. e4 e5 2. Nf3 Nc6 ..."
```

---
## pgnToTcn
```js
pgnToTcn(pgnString: string): string
```

Loads PGN movetext into Chess.js, extracts its move history, and encodes it into TCN.

**Parameters:**
- `pgnString` (string) – valid PGN movetext.

**Returns:**
- `string` – the TCN-encoded representation of the game.

**Throws:**
- `Error` if the PGN fails to load or is invalid.

**Example:**
```js
const tcn = pgnToTcn("1. e4 e5 2. Nf3 Nc6");
console.log(tcn); // mC0Kgv5Q
```

---
## `Move` Type
```ts
type Move = {
    from?: string;
    to: string;
    promotion?: "q"|"r"|"n"|"b"|"k"|"p";
    drop?: "q"|"r"|"n"|"b"|"k"|"p";
};
```
