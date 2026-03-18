---
title: Libiry2Go output formats
---
Libiry2Go generates markdown files in two different formats, depending on the _Books per_file_ setting. It uses the custom field names that are maintained in Libiry's settings menu. 

## Choose a format

| Use Case              | Recommended Format      | Setting |
| --------------------- | ----------------------- | ------- |
| Obsidian              | One file per book       | 1       |
| Logseq                | One file per book       | 1       |
| Mobile viewing        | Multiple books per file | 50-100  |
| Backup                | Multiple books per file | 100     |
| Sharing reading lists | Multiple books per file | 25-50   |
| Knowledge management  | One file per book       | 1       |

## Format 1: multiple books per file (default)

Creates batched files with multiple books:

```
libiry2go_2026-02-13_part1.md
libiry2go_2026-02-13_part2.md
```

Each file contains up to 100 books in flat format.
File naming pattern: `libiry2go_<date>_part<number>.md`.
### File structure

```markdown
# Library Catalog
Generated: 2026-02-13

---

cover: https://covers.openlibrary.org/b/isbn/9780547928227-L.jpg
booktitle: The Handmaid's Tale 
author: Margaret Atwood
isbn: 9780385490818 
rating: 5.0
language: en
tags: distopian, scifi
path: Scifi/Atwood
size: 751.5 KB
type: epub
file_created: 2024-11-10  
file_modified: 2025-02-03

cover: https://covers.openlibrary.org/b/isbn/9780441569595-L.jpg 
booktitle: Neuromancer 
author: William Gibson 
isbn: 9780441569595 
tags: 
size: 623.4 KB
type: epub
file_created: 2026-03-02
file_modified: 2026-03-11
```

### Characteristics

- Uses Libiry flat format (`field: value`)
- Books are separated by `---` (horizontal rule)
- Up to 100 books per file (configurable)
- Compatible with Libiry for viewing

### Benefits

- Compact representation
- Easy to scroll through many books
- Fewer files to manage
- Good for backup/archival purposes

## Format 2: One file per book

Creates individual files for each book:

```
Margaret Atwood - The Handmaid's Tale.md
Margaret Atwood - The Handmaid's Tale(1).md
William Gibson - Neuromancer.md
```

Each file uses YAML frontmatter format, compatible with Obsidian.

File naming pattern: `<author> - <booktitle>(<sequence number>).md`.
File name sanitization:
- Spaces → hyphens
- Special characters are removed
- Maximum 100 characters
- Duplicate handling with numbers
### File structure

```markdown
---
cover: https://covers.openlibrary.org/b/isbn/9780547928227-L.jpg
booktitle: The Handmaid's Tale 
author: Margaret Atwood
isbn: 9780385490818 
rating: 5.0
language: en
tags: distopian, scifi
path: Scifi/Atwood
size: 751.5 KB
type: epub
---

# The Handmaid's Tale 
```

### Characteristics

- Uses YAML frontmatter (Obsidian-compatible)
- One markdown file per book
- Filename derived from book title
- Content section below frontmatter (optional)
- Compatible with Libiry for viewing

### Benefits

- Full Obsidian compatibility
- Works with Dataview queries
## Fields

Both formats include these fields when available:

| Field        | Description          |     |
| ------------ | -------------------- | --- |
| cover        | Cover image URL      |     |
| booktitle    | Book title           |     |
| author       | Author name          |     |
| isbn         | ISBN-10 or ISBN-13   |     |
| tags         | Genre/category tags  |     |
| rating       | User rating (0-10)   |     |
| publisher    | Publisher name       |     |
| year         | Publication year     |     |
| series       | Series name          |     |
| series_index | Volume number        |     |
| path         | Original folder path |     |

Content sanitization:
- Backslashes in the path name → forward slashes
- Intermediate quotes in field values are removed

Read more about Libiry's [[Obsidian integration]].
