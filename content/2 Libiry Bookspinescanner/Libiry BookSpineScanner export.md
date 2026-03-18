
## Export fields

| Field      | Description                                             | Source               |
| ---------- | ------------------------------------------------------- | -------------------- |
| cover      | Cover image URL                                         | Book database        |
| booktitle  | Book title                                              | OCR + database match |
| author     | Author name                                             | Database             |
| isbn       | ISBN-10 or ISBN-13                                      | Barcode or database  |
| tags       | Add these per file and/or per shelf in BookSpineScanner | Manual entry         |
| confidence | Match confidence %                                      | OCR analysis         |
| source     | Photo source                                            | Automatic            |
| scanned    | Scan date                                               | Automatic            |

For the first five fields, you can choose your own field names:
1. Open settings
2. Scroll to "field names"
3. Customize them to match your Libiry/Obsidian setup

Example:
```
booktitle → title
author → creator
```

## Obsidian integration

Exported files work with Obsidian's Book Search plugin:
- YAML frontmatter format matches
- Cover images display correctly
- ISBN enables additional lookups

## Libiry integration

Move the export files to a folder within your Libiry library folder. 
The books in the files are shown in Libiry's book grid, alongside any digital books you might have.

### Export format 'One file per photo' (default)

Best for Libiry, batch processing and future stock keeping.
Creates a single markdown file containing all books from one scanning session.

**Example output:**
```markdown
scan_date: 2026-03-03T08:32:49.041Z
scan_source: shelf1.jpg
books_detected: 2
books_total: 2
lookup_source: all
scanner_version: 1.0.0
---
cover: https://covers.openlibrary.org/b/isbn/9780385490818-L.jpg
booktitle: The Handmaid's Tale 
author: Margaret Atwood 
isbn: 9780385490818 
tags: 
scan_confidence: 92% 
scan_preliminary: Handmaids Tale Atwood 

cover: https://covers.openlibrary.org/b/isbn/9780441569595-L.jpg 
booktitle: Neuromancer 
author: William Gibson 
isbn: 9780441569595 
tags: 
scan_confidence: 88% 
scan_preliminary: Neuromancer Gibson 
```

**Filename:** `shelf_2026-03-03_08-32-49.md`

### Export format 'One file per book'

Best for Obsidian and other personal knowledge management tools.
Creates individual markdown files for each detected book.

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

**Filename:** `shelf_2026-03-03_08-32-49(1).md`

## File splitting

When scanning many books, files are automatically split:

- Maximum 100 books per file
- Creates `shelf_part1.md`, `shelf_part2.md`, etc.
- Matches Libiry's 100-book limit per file
