# Immutable JSON object tables, typed cursors

An immutable, bounded table of JSON objects for API responses and local JSON data.
`Import jsonrows` exposes `JSONRowsTable` and independent `JSONRowsCursor` values.
There are no native or package dependencies beyond the JSON prelude.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add jsonrows --git https://github.com/BuoyBay/jsonrows.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## API at a glance

| Operation | Behavior |
| --- | --- |
| `RowCount`, `ColumnCount` | Read-only dimensions |
| `Columns()`, `ColumnName(index)`, `ColumnIndex(name)` | Union of keys, in first-seen row/key order; names are case-sensitive and indices zero-based; absent name returns -1 |
| `HasField(rowIndex, name)` | False for a missing field, True for explicit null |
| `CellKind(rowIndex, name)` | -1 for missing; otherwise `JSONItem.KindNull` through `KindObject` |
| `Cell(rowIndex, name)` | Deep copy of a present JSON value; missing throws |
| `Row(rowIndex)`, `Snapshot()` | Deep copies of a row or the entire source array |

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer jsonrows
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```


## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
