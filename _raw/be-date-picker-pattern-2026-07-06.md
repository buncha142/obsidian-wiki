---
source: conversation:2026-07-06
project: takbat-phatthalung-2569
status: raw
---

Pattern: adding a native calendar picker to a Buddhist-era (พ.ศ.) date field in html-data-editor-generated tools.

Context: coordination-log.html (from the html-data-editor skill) stores dates as free-text พ.ศ. strings (e.g. "2569-07-06"). Native `<input type="date">` only understands Gregorian years and can't display พ.ศ. directly, so it can't just replace the text field.

Solution used: keep the visible field as `<input type="text" id="ef-date">` (unchanged storage format), add a small "📅" button next to it, and a hidden `<input type="date" id="ef-date-picker">`. The button converts the current พ.ศ. text to a Gregorian ISO date (year - 543) and opens the picker via `showPicker()` (falls back to `.click()`); on `change`, the picked Gregorian date is converted back to พ.ศ. (year + 543) and written into the visible text field. Conversion is a pure regex-based `YYYY-MM-DD` split/offset — no date library needed.

This is a reusable pattern for any html-data-editor tool that stores พ.ศ. dates as text and wants a calendar picker without changing the storage/export format. ^[inferred]

## Related
- [[html-data-editor-real-file-save]]
