---
title: "jsonrows typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["JSONRowsCursor", "JSONRowsTable"]
dependencies: []
symbols: ["JSONRowsCursor", "JSONRowsTable"]
related: ["api.md", "getting-started.md", "index.md"]
---

# jsonrows typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## JSONRowsTable

`Public Class JSONRowsTable`

Immutable table of JSON objects. Returned mutable values are deep copies.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `RowCount` | `Integer` | Yes | No | — | — |
| `ColumnCount` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(source As String, maxCharacters As Integer = 1000000, maxRows As Integer = 10000, maxColumns As Integer = 1000, maxDepth As Integer = 32)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `source` | `String` | `ByVal` | Required |
| `maxCharacters` | `Integer` | `ByVal` | `1000000` |
| `maxRows` | `Integer` | `ByVal` | `10000` |
| `maxColumns` | `Integer` | `ByVal` | `1000` |
| `maxDepth` | `Integer` | `ByVal` | `32` |

Returns: no value.

### Columns

`Public Function Columns() As Array Of String`

No parameters.

#### Returns

| Type |
| --- |
| `Array Of String` |

### ColumnIndex

`Public Function ColumnIndex(name As String) As Integer`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |

### ColumnName

`Public Function ColumnName(index As Integer) As String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `index` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### HasField

`Public Function HasField(rowIndex As Integer, name As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rowIndex` | `Integer` | `ByVal` | Required |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### CellKind

`Public Function CellKind(rowIndex As Integer, name As String) As Integer`

Missing is -1; present fields use JSONItem.Kind* constants.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rowIndex` | `Integer` | `ByVal` | Required |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |

### Cell

`Public Function Cell(rowIndex As Integer, name As String) As JSONItem`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rowIndex` | `Integer` | `ByVal` | Required |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `JSONItem` |

### Row

`Public Function Row(rowIndex As Integer) As JSONItem`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rowIndex` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `JSONItem` |

### Snapshot

`Public Function Snapshot() As JSONItem`

No parameters.

#### Returns

| Type |
| --- |
| `JSONItem` |

### StringValue

`Public Function StringValue(rowIndex As Integer, name As String) As String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rowIndex` | `Integer` | `ByVal` | Required |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### NumberValue

`Public Function NumberValue(rowIndex As Integer, name As String) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rowIndex` | `Integer` | `ByVal` | Required |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### BooleanValue

`Public Function BooleanValue(rowIndex As Integer, name As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rowIndex` | `Integer` | `ByVal` | Required |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### NewCursor

`Public Function NewCursor() As JSONRowsCursor`

No parameters.

#### Returns

| Type |
| --- |
| `JSONRowsCursor` |

## JSONRowsCursor

`Public Class JSONRowsCursor`

Independent cursor, initially before the first row, then after-last at EOF.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Position` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(table As JSONRowsTable)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `table` | `JSONRowsTable` | `ByVal` | Required |

Returns: no value.

### Reset

`Public Sub Reset()`

No parameters.

Returns: no value.

### MoveNext

`Public Function MoveNext() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### MoveTo

`Public Sub MoveTo(rowIndex As Integer)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rowIndex` | `Integer` | `ByVal` | Required |

Returns: no value.

### HasField

`Public Function HasField(name As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### CellKind

`Public Function CellKind(name As String) As Integer`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |

### Cell

`Public Function Cell(name As String) As JSONItem`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `JSONItem` |

### StringValue

`Public Function StringValue(name As String) As String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### NumberValue

`Public Function NumberValue(name As String) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### BooleanValue

`Public Function BooleanValue(name As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |
