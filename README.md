# PDF, Image & Document Combiner

A small browser app that combines PDFs, images, and text extracted from DOCX, PPTX, and ODP files into one PDF. Files are processed locally in your browser; the app does not upload them or use a conversion server.

## Use it

Open the app at https://vlageez.github.io/simple-pdf-combiner/, or open `index.html` in a modern browser. The bundled `pdf-lib.min.js` library is used when present; if it is missing, the page tries to load pdf-lib from cdnjs, so that case requires an internet connection.

1. Drop files onto the box (or click to choose them): PDF, supported images, DOCX, PPTX, or ODP.
2. Drag rows — or use the ↑ / ↓ buttons — to set the output order.
3. Optionally narrow a PDF to selected pages. Office files are converted automatically.
4. Click **Combine & download** to save `combined.pdf`.

### Office document conversion

Office files are parsed in your browser. PPTX and ODP presentations produce pages containing each slide's readable text (very text-heavy slides may continue across multiple pages). DOCX text is laid out into plain pages. ODT word-processing documents are not supported; ODP here refers to presentations. The conversion is deliberately text-only: original fonts, styling, page layout, images, charts, tables' visual formatting, animations, speaker notes, and other embedded objects are not preserved. DOCX page breaks and original pagination are not retained; its output pagination is generated from the extracted text. Office-generated PDF pages are raster images, so their text is not selectable or searchable. Documents with no readable text may be rejected or produce blank presentation slides.

This is intended as a convenient way to collect document text alongside PDFs and images, not as a faithful Office renderer. For a visually accurate copy, export the document to PDF in an office suite first and add that PDF.

## Page ranges

Leave the page box blank to include every PDF page. Otherwise enter a comma-separated list:

| Input | Pages taken |
|---|---|
| *(blank)* | all |
| `3` | page 3 only |
| `1-4` | pages 1 through 4 |
| `5-` | page 5 to the end |
| `-3` | start through page 3 |
| `1-2, 7, 9-` | combinations of the above |

Out-of-range or malformed input turns the field red and disables the Combine button until it is fixed. Page ranges apply to PDFs only.

Each image becomes one page, sized to the image and scaled so its long edge fits an A4 side without upscaling.

## Features

- Drag-and-drop or file picker for PDFs, images (JPEG, PNG, SVG, GIF, WebP, BMP, AVIF, and other browser-decodable image formats), DOCX, PPTX, and ODP
- Image pages retain EXIF photo orientation; SVGs are rasterized at higher resolution
- Local text extraction from DOCX, PPTX, and ODP, with output page count shown in the file list
- Reorder by dragging, sort alphabetically, remove individual files, or clear all
- Live count of output pages and per-file error reporting
- Light and dark themes follow your system setting; works on mobile widths

## Privacy

Input files are read and processed in the browser. Office documents are not sent to a third-party conversion service. The app has no backend and does not transmit your files. When the library bundle is available locally, combining files needs no network requests; if the bundle is missing, pdf-lib's CDN fallback loads the library only.

## Limitations

- Office conversion keeps readable text, not the original document appearance. Use PDF input when visual fidelity matters.
- Office formats must be ZIP-based DOCX, PPTX, or ODP files. Encrypted documents, ZIP64 archives, unsupported compression, and archives beyond the parser's safety limits are not supported.
- Browser support for `DecompressionStream` is needed for compressed Office files; use a current browser.
- Large files are held in memory; processing may be slow or hit browser memory limits.
- Image formats are limited to what your browser can decode; unsupported files are flagged on their own row.
- Output PDFs are unencrypted, even if an input PDF was protected.
- PDF form fields, annotations, and bookmarks are not guaranteed to survive merging.

## License

Public domain. Open-source.
