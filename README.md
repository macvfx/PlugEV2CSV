# PlugEVCSVUpdater (macOS SwiftUI App and cli bash option)

A drag-and-drop macOS app that imports PlugEV receipt `.rtf` files and updates your charging totals in a CSV (comma separated values) file.

## Features
- Drag and drop `.rtf` receipts into the app window
- Manual import via file picker
- Optional watch folder with scheduled auto-scan
- Watch scan schedule options: `Hourly`, `Daily`, or `Weekly`
- Selectable watch scan start time in Settings
- Dedupes by `Date and Time` (same behavior as your scripts)
- Writes CSV in the same format (rows, blanks, summary totals)

## First Run
1. Open the app.
2. See the app layout for drag and drop.
3. Open **Settings** in the app.
4. Set **CSV Output** path (or keep default).
5. Optional: enable **Watch Folder**, pick your receipts folder, set scan period (`Hourly`/`Daily`/`Weekly`), and select scan start time.

## User Guide
- Full guide: `USER_GUIDE.md`

## Three Options Receipt Workflow
- AppleScript example for Mail rules:
  - `Save PlugEV Receipt as RTF example.scpt`
- Workflow options:
  1. Save PlugEV email receipts manually as `.rtf` files and import/scan them with this app.
  2. Set up an Apple Mail rule that runs the AppleScript to save PlugEV emails as `.rtf` into a target folder such as /Users/Shared (default in AppleScript), then configure this Mac app to watch that folder on a schedule (`Hourly`/`Daily`/`Weekly`) with your selected start time.
  3. Or, use Terminal and run the bash script

## Command Line Alternative (`plugev_parse.sh`)
If you prefer terminal workflows instead of the macOS app, use:

- `plugev_parse.sh`

Examples:
- `cd "~/Downloads"` (or wherever you saved the script)
- `./plugev_parse.sh "PlugEV Receipt.rtf"`
- `./plugev_parse.sh "/path/to/receipt1.rtf" "/path/to/receipt2.rtf"`
- `./plugev_parse.sh --csv "/path/to/output.csv" "/path/to/receipt.rtf"`

Use this when you want direct script-based processing and do not need app features like drag-and-drop UI, watch-folder scheduling, or activity log.

## Tech Notes
- Mac app parser implementation is in Swift and uses macOS `textutil` under the hood to convert RTF to text.
