# PlugEV CSV Updater User Guide

This guide is for day-to-day use of the macOS app.

## What the App Does
- Imports PlugEV `.rtf` receipt files.
- Extracts charging session data.
- Updates your CSV file.
- Prevents duplicates using `Date and Time`.
- Supports manual imports and scheduled watch-folder scans.

## Main Features
- Drag and drop receipts onto the main window.
- Import receipts from file picker.
- Scan watch folder now (manual one-time scan).
- Auto-scan watch folder on a schedule:
  - `Hourly`
  - `Daily`
  - `Weekly`
- Pick a scan start time in Settings.
- Open the output CSV directly from the app.
- Activity log with timestamped events.

## Two-Part Email-to-CSV Workflow
- AppleScript file for Apple Mail rule actions:
  - `PlugEV Mail action Applescript/Save PlugEV Receipt as RTF example.scpt`

Use either of these approaches:

1. Manual route:
- Save PlugEV email receipts manually as `.rtf`.
- Import with drag/drop or file picker, or keep receipts in the app's watch folder.

2. Automated route:
- Create an Apple Mail rule that matches PlugEV emails.
- Configure the rule to run the AppleScript above so matching emails are saved as `.rtf` in a folder.
- In this app, set that same folder as **Watch Folder**.
- Set **Scan frequency** (`Hourly`, `Daily`, or `Weekly`) and **Start time**.
- Leave the app running so scheduled scans process newly saved receipts.

## Command Line Alternative (`plugev_parse.sh`)
If you do not want to use the macOS app, you can process receipts directly via script:

- Script path: `plugev_parse.sh`

Basic usage:
1. Open Terminal.
2. Run `cd "~/Downloads"` (or where ever you saved the script).
3. Run one of:
- `./plugev_parse.sh "PlugEV Receipt.rtf"`
- `./plugev_parse.sh "/path/to/receipt1.rtf" "/path/to/receipt2.rtf"`
- `./plugev_parse.sh --csv "/path/to/output.csv" "/path/to/receipt.rtf"`

Choose script mode when you want command-line automation and do not need app UI features like watch scheduling or logs.

## Before You Start
- PlugEV receipt files in `.rtf` format.
- A target output CSV folder path where the file are written.

## First-Time Setup
1. Launch the app.
2. Open **Settings**.
3. In **CSV Output**, click **Choose CSV Location...** and pick your output file.
4. In **Watch Folder**, optionally enable **Enable watch folder**.
5. Click **Choose Watch Folder...** and select your receipts folder.
6. Set **Scan frequency** to `Hourly`, `Daily`, or `Weekly`.
7. Set **Start time**.
8. Close Settings.

## Typical Workflows

### Manual Import (Drag and Drop)
1. Drag one or more `.rtf` files into the drop zone.
2. Wait for processing to finish.
3. Check **Activity Log** for added session count.

### Manual Import (File Picker)
1. Click **Import Files...**
2. Select one or more `.rtf` files.
3. Confirm import and review **Activity Log**.

### Watch Folder Scheduled Import
1. Open **Settings** and enable watch folder.
2. Choose watch folder.
3. Set scan frequency and start time.
4. Leave the app running to allow scheduled scans.
5. Use **Scan Watch Folder Now** any time for immediate scan.

## Schedule Behavior
- `Hourly`: scans once per hour at the selected minute/second.
- `Daily`: scans once per day at the selected time.
- `Weekly`: scans once per week at the selected weekday/time anchor.
- Status text shows when watch mode is enabled and includes next scan timing.

## Output and Deduplication
- Existing CSV is loaded before write.
- New sessions are added only when `Date and Time` is not already present.
- CSV is rewritten with merged data and updated totals.

## Troubleshooting
- No files imported:
  - Confirm files are `.rtf`.
  - Confirm watch folder path is valid.
- Watch scan did not run:
  - Confirm watch is enabled.
  - Confirm app is still running.
  - Check selected schedule and start time.
- Duplicates expected but not added:
  - Duplicate key is `Date and Time` by design.
