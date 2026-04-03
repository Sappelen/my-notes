---
title: Libiry2Go output format
---
Libiry2Go generates markdown files with the custom field names that you set in Libiry's settings menu. Each file contains YAML frontmatter, compatible with Obsidian.

```
Margaret Atwood - The Handmaid's Tale.md
Margaret Atwood - The Handmaid's Tale(1).md
William Gibson - Neuromancer.md
Unknown - Renate Oude Nijeweme - Insular.md
```

File naming pattern: `<author> - <booktitle>(<sequence number>).md`. If the file's metadata are not filled in, the file name is copied from the original file.

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

## Fields

These fields when available:

| Field            | Description                                                  |     |
| ---------------- | ------------------------------------------------------------ | --- |
| cover            | Cover image URL                                              |     |
| booktitle        | Book title                                                   |     |
| author           | Author name                                                  |     |
| author_sort      | Author sort name                                             |     |
| isbn             | ISBN-10 or ISBN-13                                           |     |
| rating           | User rating (0-10)                                           |     |
| publisher        | Publisher name                                               |     |
| publication_date |                                                              |     |
| language         | Publication language                                         |     |
| pages            |                                                              |     |
| tags             | Genre/category tags                                          |     |
| series           | Series name                                                  |     |
| series_index     | Volume number                                                |     |
| translator       |                                                              |     |
| illustrator      |                                                              |     |
| description      |                                                              |     |
| notes            |                                                              |     |
| file             | Original file name, including folder path                    |     |
| size             |                                                              |     |
| type             |                                                              |     |
| created          | Creation date of the book - for tracking your reading habits |     |
| updated          | Modified date of the book - for tracking your reading habits |     |
| generated        | Date the markdown file was generated                         |     |

Content sanitization:
- Backslashes in the path name → forward slashes
- Intermediate quotes in field values are removed

Read more about Libiry's [[Obsidian integration!!!]].
