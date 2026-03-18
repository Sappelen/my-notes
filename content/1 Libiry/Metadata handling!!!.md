---
title: Metadata handling
---
Libiry extracts and manages book metadata from various sources and formats.

## Metadata fields

Libiry supports 13 metadata fields, following the Goodreads CSV format: 

| Field | Goodreads Equivalent | Description |
|-------|---------------------|-------------|
| `cover` | - | Cover image URL or path |
| `booktitle` | Title | Book title |
| `author` | Author | Author name |
| `isbn` | ISBN | ISBN-10 or ISBN-13 |
| `rating` | My Rating | User rating (0-10 internally, 0-5 displayed) |
| `publisher` | Publisher | Publisher name |
| `year` | Year Published | Publication year |
| `language` | - | Language code (extra field) |
| `tags` | Bookshelves | Genre/category tags |
| `series` | - | Series name (extra field) |
| `series_index` | - | Volume number in series |
| `description` | My Review | Book summary or review |
| `notes` | Private Notes | Personal notes |

All field names are configurable in `customize.txt`.

## Metadata extraction

### EPUB Files

Metadata is read from the OPF file inside the EPUB:

```xml
<metadata>
  <dc:title>The Book Title</dc:title>
  <dc:creator>Author Name</dc:creator>
  <dc:subject>fiction</dc:subject>
  <dc:identifier>978-1234567890</dc:identifier>
</metadata>
```

### PDF files

Metadata is read from the PDF's document information dictionary:

- Title → `booktitle`
- Author → `author`
- Subject → `description`
- Keywords → `tags` (comma-separated)

### MOBI/AZW Files

Basic metadata is extracted using the `mobi` library:

- Title → `booktitle`
- Author → `author`
- Tags → from OPF sidecar file

### Comic files (CBR/CBZ)

Metadata is read from `ComicInfo.xml`:

```xml
<ComicInfo>
  <Title>Comic Title</Title>
  <Writer>Author Name</Writer>
  <Genre>Action, Adventure</Genre>
</ComicInfo>
```

### Markdown files

```yaml
---
cover: "[[cover.jpg]]"
booktitle: The Book Title
author: Author Name
isbn: 978-1234567890
tags:
  - fiction
  - fantasy
rating: 4
---
```

The YAML frontmatter:
- Supports the Obsidian link syntax: `[[url]]` or `![[url]]`
- Uses arrays for tags: `tags: [fiction, fantasy]`. Multi-line tags are also suported
- Numbers are parsed as integers

## Tag management

### Reading tags

Tags are read from (in priority order):
1. OPF sidecar file (if exists)
2. Embedded metadata in ebook
3. Markdown content

### Writing tags

Tags are written to:
- **EPUB**: Embedded `<dc:subject>` elements
- **MOBI/AZW/AZW3**: OPF sidecar file
- **PDF**: Keywords field (or OPF sidecar if problematic)
- **CBZ**: `ComicInfo.xml`
- **CBR**: OPF sidecar file
- **Markdown**: In file content

### Tag format

Tags are stored as:
- Comma-separated string in some formats
- Multiple `<dc:subject>` elements in EPUB/OPF
- Array in YAML frontmatter

## Cover handling

### Cover sources (priority order)

1. **Embedded cover** - Extracted from ebook file
2. **Cover field** - URL or path in metadata
3. **Online lookup**:
   - Open Library (by ISBN or title+author)
   - Google Books (by ISBN or title+author)
   - Europeana (European books)

### Cover display

- **Thumbnails cached** in SQLite database
- **Cache cleared** on startup for fresh covers
- **Fallback display** shows author + title text

### Cover field formats

```yaml
# URL
cover: https://example.com/cover.jpg

# Local path
cover: ./covers/book.jpg

# Obsidian syntax
cover: "[[cover.jpg]]"
cover: "![[cover.jpg]]"
```

## Duplicate detection

The Twins filter detects duplicates using:

### ISBN matching

Exact match on ISBN-10 or ISBN-13

### Title + author matching

Normalization process:
1. Convert to lowercase
2. Remove articles: "the", "a", "an", "de", "het", "een"
3. Remove author suffixes: "jr", "sr", "phd"
4. Sort author name parts alphabetically
5. Compare normalized strings

Example:
- "The Handmaid's Tale" by "Margaret Atwood"
- "Handmaid's Tale" by "Atwood, Margaret"
- Both normalize to the same value → detected as duplicate

## Field name customization

Map Libiry fields to your existing metadata:

```ini
# For Obsidian
Field name booktitle: title
Field name tags: tags

# For custom setups
Field name booktitle: book_title
Field name author: writer
```

This ensures compatibility with:
- Goodreads exports
- Obsidian plugins (Book Search, Booksidian)
- Calibre libraries
- Custom database schemas
