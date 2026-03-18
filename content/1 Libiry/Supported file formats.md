---
title: Supported file formats
---
Libiry supports a wide range of ebook and document formats.

## Ebook formats

### EPUB (.epub)

The most common ebook format, fully supported.

| Feature | Support |
|---------|---------|
| Read metadata | ✓ Full support |
| Extract cover | ✓ Full support |
| Write tags | ✓ Full support |

Tags are stored in the EPUB's OPF metadata using `<dc:subject>` elements.

### MOBI/AZW/AZW3 (.mobi, .azw, .azw3)

Amazon Kindle formats.

| Feature | Support |
|---------|---------|
| Read metadata | ✓ Full support |
| Extract cover | ✓ Full support |
| Write tags | ✓ Via OPF sidecar |

Tags are stored in an OPF sidecar file (e.g., `book.opf` for `book.mobi`) because these formats don't support direct metadata editing.

### PDF (.pdf)

Portable Document Format.

| Feature | Support |
|---------|---------|
| Read metadata | ✓ Full support |
| Extract cover | ✓ First page thumbnail |
| Write tags | ✓ In keywords field or OPF sidecar |

Some PDFs with encryption or complex structures use OPF sidecar files for tag storage. Use the [PDF Tag Checker](PDF%20Tag%20Checker.md) utility to identify these.

## Comic Formats

### CBZ (.cbz)

Comic book archive (ZIP-based).

| Feature | Support |
|---------|---------|
| Read metadata | ✓ From ComicInfo.xml |
| Extract cover | ✓ First image |
| Write tags | ✓ In ComicInfo.xml |

Metadata is stored in `ComicInfo.xml` inside the archive.

### CBR (.cbr)

Comic book archive (RAR-based).

| Feature | Support |
|---------|---------|
| Read metadata | ✓ Basic support |
| Extract cover | ✓ First image |
| Write tags | ✓ Via OPF sidecar |

RAR archives are read-only, so tags are stored in OPF sidecar files.

## Document Formats

### Markdown (.md)

Full markdown support with two metadata formats.

| Feature | Support |
|---------|---------|
| Read metadata | ✓ YAML or flat format |
| Extract cover | ✓ From cover field |
| Write tags | ✓ Full support |

#### YAML Frontmatter (Obsidian-compatible)

```yaml
---
cover: "cover.jpg"
booktitle: "The Book Title"
author: "Author Name"
isbn: "978-1234567890"
tags: [fiction, fantasy]
rating: 8
---

Book content here...
```

#### Flat Format (Libiry/BookSpineScanner)

```markdown
[cover]: https://example.com/cover.jpg
[booktitle]: The Book Title
[author]: Author Name
[isbn]: 978-1234567890
[tags]: fiction, fantasy
[rating]: 8

---

[cover]: https://example.com/cover2.jpg
[booktitle]: Another Book
[author]: Another Author
```

The flat format supports multiple books per file (up to 100 for performance).

## OPF sidecar files

For formats that don't support direct tag editing, Libiry uses OPF (Open Packaging Format) sidecar (buddy) files. This includes:

- **MOBI/AZW/AZW3** - Always uses OPF buddy
- **CBR** - Always uses OPF buddy (RAR is read-only)
- **Problematic PDFs** - Uses OPF buddy when direct editing fails
- **All other formats** - RTF, MP3, TXT, DOC, etc. automatically use OPF buddy

### How it works

1. When you edit tags on `book.mobi`, Libiry creates `book.opf`
2. The OPF file stores metadata in XML format
3. On reading, Libiry checks for OPF file first, then embedded metadata

### OPF structure

```xml
<?xml version="1.0" encoding="UTF-8"?>
<package xmlns="http://www.idpf.org/2007/opf" version="3.0">
  <metadata xmlns:dc="http://purl.org/dc/elements/1.1/">
    <dc:subject>fiction</dc:subject>
    <dc:subject>fantasy</dc:subject>
    <dc:subject>adventure</dc:subject>
  </metadata>
</package>
```

## Other file formats

Any file type can be added to your library. For formats not listed above (such as `.rtf`, `.mp3`, `.txt`, `.doc`, etc.), Libiry automatically uses OPF buddy files for tag storage.

| Feature | Support |
|---------|---------|
| Display in grid | ✓ Shows filename |
| Read metadata | Filename only |
| Write tags | ✓ Via OPF buddy file |

Simply add the file extension to `selected types.txt` and Libiry will handle it.

**Note:** `.opf` files themselves are not displayed as books (they are buddy files for other formats).

## File Type Filtering

Configure which file types are displayed in `selected types.txt`:

```
.epub
.mobi
.azw
.azw3
.pdf
.cbr
.cbz
.md
.rtf
.mp3
```

To add a new type, add its extension on a new line.

## Format Detection

Libiry detects file formats by extension, not by content inspection. Ensure your files have correct extensions.

## Cover Extraction Priority

1. **Embedded cover** in ebook metadata
2. **First image** for comics (CBR/CBZ)
3. **First page** thumbnail for PDFs
4. **Cover field** in markdown files
5. **Online lookup** from Open Library, Google Books, Europeana

## Performance Notes

- Large PDFs may take longer to extract covers
- Comics with many images are processed efficiently (only first image)
- Markdown files with >100 books are split for performance
- Thumbnail cache speeds up repeated access
