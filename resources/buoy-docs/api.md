---
title: "jsonrows API contracts"
summary: "Usage and behavioral contracts for jsonrows."
category: "Reference"
symbols: ["JSONRowsTable", "JSONRowsCursor"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# JSONRows 0.1.0

An immutable, bounded table of JSON objects for API responses and local JSON data.
`Import jsonrows` exposes `JSONRowsTable` and independent `JSONRowsCursor` values.
There are no native or package dependencies beyond Buoy's JSON prelude.

## API

`New JSONRowsTable(source, maxCharacters = 1000000, maxRows = 10000,
maxColumns = 1000, maxDepth = 32)` parses a JSON array containing only objects.
Rows may have different fields and different types in the same column. Empty
arrays and empty objects are valid. Malformed JSON throws `JSONException`;
shape, type, bounds and budget violations throw `InvalidArgumentException`.
A non-object row reports its zero-based array index, for example
`JSONRows row at index 1 must be an object` identifies the second array element.

| Operation | Behavior |
| --- | --- |
| `RowCount`, `ColumnCount` | Read-only dimensions |
| `Columns()`, `ColumnName(index)`, `ColumnIndex(name)` | Union of keys, in first-seen row/key order; names are case-sensitive and indices zero-based; absent name returns -1 |
| `HasField(rowIndex, name)` | False for a missing field, True for explicit null |
| `CellKind(rowIndex, name)` | -1 for missing; otherwise `JSONItem.KindNull` through `KindObject` |
| `Cell(rowIndex, name)` | Deep copy of a present JSON value; missing throws |
| `Row(rowIndex)`, `Snapshot()` | Deep copies of a row or the entire source array |
| `StringValue`, `NumberValue`, `BooleanValue` `(rowIndex, name)` | Require the exact JSON type; no coercion, defaulting or null conversion |
| `NewCursor()` | Independent cursor retaining this immutable table |

Cursor `Position` starts at -1. `MoveNext()` moves to the first/next row and
returns True there; at EOF it returns False and stays at `RowCount`. `Reset()`
returns to -1; `MoveTo(index)` requires an existing row. Cursors offer the same
field/accessor methods without the row-index argument. Access before-first or
after-last throws. Empty-table `MoveNext()` returns False at position 0.

All arrays and mutable JSON values returned by the table are independent copies,
including nested objects/arrays. Table/cursor assignment still shares the same
object; use `NewCursor()` for independent positions. There are no editing APIs.

## Numbers and limits

Buoy JSON stores **every number as Double**. `NumberValue` preserves that Double,
and defensive JSON serialization uses the runtime's shortest round-trip format.
An integer token above 2^53 can already be rounded when parsed. This package
does not reconstruct original number tokens, expose exact Int64/decimal values or
silently convert strings to numbers. Encode exact large identifiers as strings.
Duplicate source keys use Buoy's JSON contract: last value wins, first position
remains. Use explicit key/type validation for schemas that forbid duplicates.

Character count is checked before allocation of the character preflight array.
Container nesting is checked before `Json.Parse`, ignoring brackets in escaped
strings. Depth counts the outer array as one and row objects as two. Hard ceilings
are 16,000,000 characters, 1,000,000 rows, 10,000 union columns and depth 128.
The default budgets are deliberately smaller. Row/column budgets may be zero.
The character limit bounds the whole parse, while row/column limits are validated
after parsing; this is not a streaming parser. Column union uses an exact linear
lookup, with worst-case O(total field count × union columns) comparisons. A copy
costs O(the returned JSON subtree), bounded by the original accepted input.

## Example and verification

Maintainers run the private validation suite before release. See the repository README for public build instructions.

This is a focused independent adapter inspired by JsonRowSet. SQL metadata,
database conversions, mutations/SaveRow, heterogeneous Variant coercion,
streaming and reactive UI bindings are outside its contract. See
provenance for upstream evidence and intentional differences.


[Typed API](typed-api.md) · [Getting started](getting-started.md)
