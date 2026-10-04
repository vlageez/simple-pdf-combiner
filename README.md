# PDF Combiner

A single-file web app that merges PDFs entirely in your browser. No server, no upload, no build step — your files never leave your device.

## Use it

Double-click `index.html`, or open it in any modern browser. It runs fine from `file://`.

1. Drop PDFs onto the box (or click to pick them)
2. Drag rows — or use the ↑ / ↓ buttons — to set the order
3. Optionally narrow each file to a page range
4. **Combine & download** → saves `combined.pdf`

## Page ranges

Leave the page box blank to include every page. Otherwise enter a comma-separated list:

| Input      | Pages taken                |
|------------|----------------------------|
| *(blank)*  | all                        |
| `3`        | page 3 only                |
| `1-4`      | pages 1 through 4          |
| `5-`       | page 5 to the end          |
| `-3`       | start through page 3       |
| `1-2, 7, 9-` | combinations of the above |

Out-of-range or malformed input turns the field red and disables the Combine button until it's fixed.

## Features

- Drag-and-drop or file picker; non-PDF files are ignored
- Reorder by dragging, sort alphabetically, remove individual files, clear all
- Live count of the pages that will end up in the output
- Per-file error reporting — a damaged or locked PDF is flagged on its own row instead of failing the whole batch
- Encrypted PDFs are read when possible; if one can't be opened, remove its password first
- Light and dark themes follow your system setting; works on mobile widths

## Privacy

Everything happens in the page: files are read with the File API, merged in memory, and handed back as a blob download. There is no backend and nothing is transmitted. To verify, open DevTools → Network and merge a file — you'll see no requests.

## Offline use

The page loads [pdf-lib](https://pdf-lib.js.org/) 1.17.1 from a CDN, so the *first* load needs internet. To make it work fully offline, download the library next to `index.html`:

```bash
curl -O https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js
```

Then change the script tag in `index.html` to:

```html
<script src="pdf-lib.min.js"></script>
```

## Hosting

It's one static HTML file, so any static host works — GitHub Pages, Netlify, S3, or a folder on a shared drive. Nothing to configure.

## Limitations

- Large PDFs are held in memory; merging several hundred-megabyte files may be slow or hit browser memory limits
- Output PDFs are unencrypted, even if an input was protected
- Form fields, annotations, and bookmarks are not guaranteed to survive the merge
- Requires a browser with the File API and `async`/`await` (any release from the last several years)

## License

Public domain — do whatever you like with it.
