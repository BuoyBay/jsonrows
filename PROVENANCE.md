# JSONRows provenance

Inspected [npalardy/JsonRowSet](https://github.com/npalardy/JsonRowSet) at commit
`df03b5de7fa2b277653b0d418758b29b02f0962f`.
The upstream README describes an adapter for fairly flat API arrays of objects.
Actual source inspected: `JSONRowset/JSONBackedRowSet.xojo_code`,
`JSONBackedRow.xojo_code`, `JsonBackedColumn.xojo_code` and both iterator classes.
The upstream LICENSE is MIT, copyright 2025 npalardy, retained in
`UPSTREAM-LICENSE.txt`. This implementation copies no upstream code or assets.

The upstream provides database-like column wrappers, conversion operators,
iteration, navigation, edit/save/remove methods and Variant values. JSONRows
instead provides an immutable snapshot, deterministic heterogeneous key union,
explicit missing/null distinction, exact JSON-type reads and independent cursors.
It supports nested values through defensive JSONItem copies without pretending
those values are database column types. It is not a drop-in Xojo RowSet.

Local references read: Buoy 0.72.0 `json.md`, `map.md`, the project AGENTS.md and
existing package/test layouts. The actual compiler verifies all provided Buoy
sources. Numeric behavior follows the documented JSONItem Double representation;
the upstream's integer/currency/date conversion surface is deliberately omitted.
