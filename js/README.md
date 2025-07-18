# Chess TCN JavaScript

A JavaScript library for encoding and decoding TCN, a move format used by **Chess.com**'s API.

## Installation

```bash
npm install chess-tcn
```

## Quick Start

```js
import { decodeTCN, encodeTCN, tcnToPgn, pgnToTcn } from "chess-tcn";

const tcnString = "mC0Kgv7Tbq5Qlt9IqHT7cM1TMFWOHs2MFwZRfm6Eeg";

// Decode a raw TCN string into move objects
const moves = decodeTCN(tcnString);
console.log("Decoded moves:", moves);

// Encode those move objects back into TCN
const newTcn = encodeTCN(moves);
console.log("Re-encoded TCN:", newTcn);

// Convert a raw TCN string to PGN
const pgn = tcnToPgn(tcnString);
console.log("PGN:", pgn);

// Convert PGN back into a TCN string
const newTcnString = pgnToTcn(pgn);
console.log("New TCN string:", newTcnString);
```

## API Reference

See [API.md](/js/API.md) for full details.
