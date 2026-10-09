# Gujarati Shrimad Rajchandra

Metadata: Granth / Gujarati / Dravyanuyog, Name and Author Shrimad Rajchandra. LLM OCR; ignore_bookmarks=true. No header_regex or strip_regex.

1000 physical PDF pages. Include 70–908. Exclude front matter and contents (1–69), back reference indexes (909–1000), portrait pages 102, 208, 381, 715, 732, and the half-title 862. Keep text-bearing pages with portrait backgrounds and handwritten text on page 436. Twenty-four explicit sections follow printed headings/index; ranges use physical PDF pages, not printed page numbers. The final notebooks change mid-page, so remain one section.

## Crop limitation

The saved crop is top 6.5%, bottom 4%, prioritizing preservation of body text. The current crawler supports one crop per PDF. On ordinary pages this crop leaves the running book/year heading and page number. Top 8.3% removes ordinary headers, but clips the first body line on pages 240–247; page 239 is a section-opening page without that running header and does not need the smaller crop. Pages 240–247 need top 6.5%. Header and font bounding boxes overlap more than the visible ink, so these conclusions are based on rendered images, not text bounding boxes alone.

Visually checked pages 71, 200, 240, 247, 300, 400, 500, 621, 700, 800, 900, 726. At 8.3%, ordinary sample headers were removed and body retained; 240 and 247 visibly lost the first line. The side-by-side 6.5% comparison on 240 preserves that line. Bottom 4% retains low footnotes/text (including 726); bottom 5% can clip them. This is a conservative config, not a claim that all headers are gone. Clean cropping throughout needs page-specific crop support or a layout-normalized PDF; neither is introduced here.
