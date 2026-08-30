---
title: 4 Libiry2Go
---
Libiry2Go scans your library and creates markdown files containing book data. Perfect for creating mobile-friendly book lists, Obsidian vaults or backup catalogs. These files can be:
- Viewed on any device with a markdown reader
- Imported into Obsidian
- Used as a portable backup of your library catalog
- Shared with others as a reading list

You start it with the 'Libiry apps' button on Libiry's main screen.

## Key features

- **Scans entire folder hierarchies**
- **Multiple formats** - Supports EPUB, MOBI, PDF, CBR, CBZ and more
- **Field compatibility** - Uses the same field names as Libiry

Each Libiry2Go  file contains YAML frontmatter, compatible with Obsidian.

```
Margaret Atwood - The Handmaid's Tale.md
Margaret Atwood - The Handmaid's Tale(1).md
William Gibson - Neuromancer.md
Renate Oude Nijeweme - Insular.md
```

The file naming pattern is `<author> - <booktitle>(<sequence number>).md`. If the author and booktitle are empty, the book file name is copied.

File name sanitization:
- Spaces → hyphens
- Special characters are removed
- Maximum 100 characters
- Duplicate handling with numbers
## When to use Libiry2Go

| Scenario                                      | Use Libiry2Go?                             |
| --------------------------------------------- | ------------------------------------------ |
| Create book library for mobile use            | Yes                                        |
| Create book notes for Obsidian                | Yes                                        |
| Store your e-books inside your Obsidian vault | Yes, but Align Book Data is also an option |
| Backup library metadata                       | Yes                                        |
| Share reading list                            | Yes                                        |
| Browse books visually                         | No; use the complete book library instead  |
| Edit book metadata                            | No; use the complete book library instead  |
