---
title: 6 Integration with other tools
---
## Integration philosophy

Libiry uses open standards for maximum compatibility:
- **Markdown files** - Universal format
- **YAML frontmatter** - Standard format
- **Folder structure** - No proprietary database
- **Goodreads fields** - Industry-standard field names

## Supported integrations

| Tool                                    | Integration Type                                  |
| --------------------------------------- | ------------------------------------------------- |
| [Obsidian](6.1%20Obsidian%20integration.md)   | Shared library folder and book data               |
| [Calibre](6.3%20Calibre%20integration.md)     | Shared library folder, partially shared book data |
| [Goodreads](6.2%20Goodreads%20integration.md) | CSV import/export format                          |
## Integration matrix

| Feature          | Obsidian | Calibre | Goodreads |
| ---------------- | -------- | ------- | --------- |
| Shared library   | ✓        | ✓       | ✗         |
| Shared book data | ✓        | ✗       | ✗         |
| Import book data | ✓        | partial | partial   |
| Export book data | ✓        | partial | ✓         |
| Sync tags        | ✓        | partial | ✓         |
| Cover images     | ✓        | ✓       | ✗         |
