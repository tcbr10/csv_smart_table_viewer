# CSV Smart Table Viewer

A standalone, browser-only CSV viewer with global search, per-column filters, typed sorting, multi-column sorting, and virtualized rows.

## Hosted app

After GitHub Pages is enabled and the deployment succeeds, open:

https://tcbr10.github.io/csv_smart_table_viewer/

CSV files and pasted data are processed locally in your browser. The app does not send their contents to a server. GitHub hosts the HTML page; data processing runs in an embedded Web Worker.

## One-time GitHub Pages setup

1. Open https://github.com/tcbr10/csv_smart_table_viewer/settings/pages
2. Under **Build and deployment**, set **Source** to **GitHub Actions**.
3. The workflow runs automatically when a commit is pushed to `main`.
4. If the first run happened before Pages was enabled, open the repository's **Actions** tab, select **Deploy GitHub Pages**, and choose **Run workflow** on `main` (or rerun the failed run).
5. Wait for the deployment to succeed, then open the hosted app URL above.

Workflow runs: https://github.com/tcbr10/csv_smart_table_viewer/actions/workflows/pages.yml

The workflow publishes only `index.html` and a `.nojekyll` marker, not repository documentation or development files. It uses GitHub's Pages actions with `contents: read`, `pages: write`, and `id-token: write` permissions. Subsequent pushes to `main` update the site automatically.

## Offline use

Download the raw `index.html` file and open it directly in a modern desktop browser. No server, build step, dependencies, or internet connection is required by the app.

## Features

- Open a local file, drag and drop it, or paste CSV/TSV.
- Auto-detect comma, semicolon, tab, and pipe delimiters; optional header row.
- UTF-8, Windows-1252, Windows-1255 (Hebrew), and UTF-16 import options.
- Global search and AND-combined column filters.
- Click headers to cycle ascending, descending, and unsorted; Shift-click for multi-column sorting.
- Automatic text, number, and ISO-date type inference with manual overrides.
- Full cell inspection by double-click and filtered/sorted CSV export.
- System light/dark styling and a built-in 100,000-row demo.

## Performance and limitations

The worker decodes files in 512 KiB chunks and owns the full dataset. The UI renders only a viewport-sized row window. Search is debounced, and superseded query results are discarded.

100,000 records were tested during development. Practical capacity depends on available RAM, column count, and cell size; the full parsed dataset remains in memory. Rows are virtualized, but columns are not, and there is a 512-column safety limit. Browser testing was performed in Chromium.

Import settings apply to the next import. Reset View clears search, filters, and sorting while retaining column types. There is no session persistence. Optional export formula protection modifies values with certain leading characters and is not a complete spreadsheet security boundary.
