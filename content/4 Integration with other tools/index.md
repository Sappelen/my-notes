---
title: 4. Integration with other tools
---

Double clicking a book in Libiry will open it in your default reading app. But there are more ways in which other tools work well with Libiry.

## Some use cases

- Use the [[Obsidian integration]] to write book notes or visualise your library or reading progress
- Use the [[Calibre integration]] for ebook management
- Use the [[Goodreads integration]] to maintain your book metadata

## Supported integrations

| Tool | Integration Type | Documentation |
|------|-----------------|---------------|
| [Obsidian](Obsidian%20integration.md) | Markdown files, YAML frontmatter | [Guide](Obsidian%20integration.md) |
| [Calibre](Calibre%20integration.md) | Shared library folder, metadata | [Guide](Calibre%20integration.md) |
| [Goodreads](Goodreads%20integration.md) | CSV import/export format | [Guide](Goodreads%20integration.md) |

## Integration philosophy

Libiry uses **open, file-based standards** for maximum compatibility:

- **Markdown files** - Universal text format
- **YAML frontmatter** - Standard metadata format
- **OPF files** - EPUB/ebook standard
- **Folder structure** - No proprietary database
- **Goodreads fields** - Industry-standard field names

## Quick integration matrix

| Feature              | Obsidian | Calibre | Goodreads |
| -------------------- | -------- | ------- | --------- |
| Share library folder | ✓        | ✓       | ✗         |
| Import metadata      | ✓        | partial | partial   |
| Export metadata      | ✓        | partial | ✓         |
| Sync tags            | ✓        | partial | ✓         |
| Cover images         | ✓        | ✓       | ✗         |

## Field Mapping

Libiry fields can be mapped for use in other tools by using field names.

| Libiry        | Obsidian      | Calibre  | Goodreads     |
| ------------- | ------------- | -------- | ------------- |
| `booktitle`   | `title`       | Title    | Title         |
| `author`      | `author`      | Authors  | Author        |
| `isbn`        | `isbn`        | ISBN     | ISBN          |
| `tags`        | `tags`        | Tags     | Bookshelves   |
| `rating`      | `rating`      | Rating   | My Rating     |
| `description` | `description` | Comments | My Review     |
| `notes`       | `notes`       | -        | Private Notes |

All field names are configurable in the settings.

