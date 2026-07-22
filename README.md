# Azure Config Editor

A single-file, offline editor for Azure App Configuration exports. Open `index.html` directly in a browser — no install, no server, no build step.

<img width="2556" height="624" alt="image" src="https://github.com/user-attachments/assets/160cea2c-972c-4f2e-8a7e-07cc34d82362" />


## File format

This tool works with the **KVSet** JSON format used by Azure App Configuration's Import/Export feature (Portal → *Export* → format `KVSet`). Each entry looks like:

```json
{
  "key": "App:LogLevel",
  "value": "Debug",
  "label": "Dev",
  "content_type": "",
  "tags": {}
}
```

The whole file is `{ "items": [ ... ] }`. Other Azure App Configuration export shapes (e.g. the flat hierarchical JSON export, or `.properties`/`.yaml` exports) are **not** supported.

A ready-to-use sample is included: `sample-demo.json` (fictional values, no real secrets).

## Features

- **Overview** — a pivot table: rows are keys, columns are labels, cells are values. Missing key/label combinations show as "click to add" so gaps are obvious at a glance.
- **Edit** — click a cell to edit its value inline. The "⋯" button per cell edits `content_type` and `tags`. "✕" clears a value or deletes an entire key/label.
- **Compare labels** — pick two labels and see every key present in one but missing in the other, then copy the missing ones across in one click (value + content_type + tags).
- **Open/Save JSON** — in Chrome/Edge, "Save" writes back to the same file you opened (File System Access API). Other browsers fall back to a file picker for opening and a download for saving.
- **Import/Export CSV** — export the current grid as `Key,<label1>,<label2>,...` for a quick look in Excel, or import a CSV back. CSV only carries values — `content_type` and `tags` are not preserved through a CSV round-trip.

## Limitations

- Only understands the KVSet `items` array shape — no support for nested/hierarchical config formats.
- No connection to Azure — this is purely a local file editor. Getting data in/out of App Configuration is a separate manual export/import step in the Portal or CLI.
- Rename of a key or label uses the browser's native prompt dialog.
