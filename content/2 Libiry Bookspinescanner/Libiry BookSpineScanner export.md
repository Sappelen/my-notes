
## Export fields

| Field      | Description                         | Source                   |
| ---------- | ----------------------------------- | ------------------------ |
| cover      | Cover image URL                     | Book database            |
| booktitle  | Book title                          | OCR + database match     |
| author     | Author name                         | Book database            |
| isbn       | ISBN-10 or ISBN-13                  | Barcode or book database |
| tags       | Add these per book and/or per shelf | Manual entry             |
| confidence | Match confidence %                  | OCR analysis             |
| source     | Photo source                        | Automatic                |
| scanned    | Scan date                           | Automatic                |


## Export formats

### One file per book

- One '.md' file per book
- All metadata in YAML frontmatter
- Compatible with Obsidian, Logseq, Libiry and any other text editor or reader
- Download as ZIP when exporting multiple books

For the first five fields, you can choose your own field names:
- Open settings
- Scroll to "field names"
- Customize them to match your Libiry/Obsidian setup

Example:
```
booktitle → title
author → creator
```

## Obsidian integration

Exported files work with Obsidian's Book Search plugin:
- The YAML frontmatter format matches
- The cover images display correctly
- ISBN enables additional lookups

## Libiry integration

Move the export files to a folder within your Libiry library folder. 
The books in the files are shown in Libiry's book grid, alongside any digital books you might have.

### Export format

For each detected book, a markdown file is created with YAML frontmatter.

**Example output:**
```markdown
---
cover: https://covers.openlibrary.org/b/isbn/9780385490818-L.jpg
booktitle: The Handmaid's Tale 
author: Margaret Atwood 
isbn: 9780385490818 
tags: 
source: "BookSpineScanner"
scanned: "2026-02-13"
---

# The Handmaid's Tale 

```
