# Shrimad Rajchandra — ingestion decisions

Source: https://vitragelibrary.org/documents/default.aspx?f=shastra/pdf/Shrimad%20Rajchandra.pdf

The downloaded Hindi scan has 1,068 physical PDF pages. Metadata inherits
`category: Granth`, `language: hi`, and `Anuyog: Dravyanuyog` from its parent
folders. The work name and author are both `Shrimad Rajchandra`.

## Processing

- `ocr_engine: llm`, `ignore_bookmarks: true`.
- Retain Hindi, Sanskrit, and Prakrit verse blocks.
- Crop **2% top / 1% bottom**. No horizontal cropping or spread splitting.
- Scan registration varies: an experimental 6.5% top / 3% bottom crop
  intersected body text, letter dates, and bottom text on sample pages.
  A single crop cannot safely remove every running header in this PDF.
  The conservative crop preserves text; LLM heading classification and
  anchored header cleanup remove the remaining running headers after OCR.
- Header cleanup handles the book title, age/year headers, and later
  collection titles. `strip_regex` also removes these as complete lines
  within a multiline prose block, without discarding its remaining text.

## Content and exclusions

Use physical, 1-based, inclusive page bounds from `sub_sections`.

- Pages 1–73: title/publication pages, introductory material, contents,
  an illustration, a blank scan, and a half-title; outside the content ranges.
- Pages 74–933: early writings, Bhavanabodh, Mokshmala, age/year groups,
  Updesh Nondh, Updesh Chhaya, and Vyakhyansaar 1–2.
- Page 934: half-title for Abhyantar Parinam Avalokan; outside the ranges.
- Pages 935–986: Abhyantar Parinam Avalokan, including Sansmaran Pothi 1–3.
  Keep these together because the notebooks change in the middle of physical
  pages, and the scan repeats pages around the third notebook's opening.
- Pages 987–1068: blank scan and reference appendices/indexes; outside the ranges.
- `skip_pdf_pages`: portraits **108, 214, 220, 408, 776, 778, 798**;
  blank scans **111, 217, 221, 799**.
- Text-bearing diagrams remain included, including pages 109, 165, 289, and 754.

There are **24 non-overlapping sections and 901 selected physical pages**.
Section openings were checked visually against the printed contents and
page headings. The scan includes repeated pages and gaps in its printed
pagination; do not calculate PDF bounds using a constant printed-page offset.
The 30th-year group begins at PDF page 685, whose printed pagination jumps
from the preceding scan. The configs do not reconstruct missing source pages.

## Sample verification

Inspected and processed physical PDF pages **74, 100, 200, 300, 400, 500,
600, 700, 850, 950** with the final crop, the repository's Gemini
`gemini-2.5-flash` extraction function, and `GranthParagraphGenerator`.

- Compared original upper/lower page regions to ensure the final crop
  preserves body text and footnotes.
- Reviewed actual extracted blocks and generated paragraphs: running headers
  and footer stamps were absent from resulting prose. Page 400's running
  year header was returned as prose and removed by the configured cleanup.
- Page 74 is verse-focused: it produces no prose paragraphs; its verse blocks
  are retained by the configured `verses` list.
- Confirmed effective inherited metadata, engine, crop, and bookmark settings
  using the repository loaders. Checked JSON, regex syntax, section bounds,
  non-overlap, and portrait/blank exclusions.

This verifies ten samples, not full-document OCR. No OpenSearch indexing or
full-document LLM batch job was run. The local PDF is ignored by Git, as in
the rest of this configs repository; the crawler can download it via `file_url`.
