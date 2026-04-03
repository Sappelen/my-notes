---
title: 4. Libiry2Go
---
Libiry2Go scans your library and creates markdown files containing book metadata. Perfect for creating mobile-friendly book lists, Obsidian vaults or backup catalogs. These files can be:
- Viewed on any device with a markdown reader
- Imported into Obsidian
- Used as a portable backup of your library catalog
- Shared with others as a reading list
## Key features

- **Scans entire folder hierarchies**
- **Multiple formats** - Supports EPUB, MOBI, PDF, CBR, CBZ, and more
- **Field compatibility** - Uses the same field names as Libiry
- **Offline functionality** - No internet required
## Quick start

### Windows GUI

1. Run `Libiry2Go.bat`
2. Select your book folder
3. Choose an output location
4. Click Generate

### Command line

```bash
# 50 books per file
python libiry2go.py "C:\Books" "C:\Output" 50
```

## When to use Libiry2Go

| Scenario                                     | Use Libiry2Go?                                                                 |
| -------------------------------------------- | ------------------------------------------------------------------------------ |
| Create book library for mobile use           | Yes                                                                            |
| Create Obsidian book vault                   | Yes                                                                            |
| Store your ebooks inside your Obsidian vault | Yes, but storing all your book metadata in the sidecar files is also an option |
| Backup library metadata                      | Yes                                                                            |
| Share reading list                           | Yes                                                                            |
| Browse books visually                        | No; use the complete book library instead                                      |
| Edit book metadata                           | No; use the complete book library instead                                      |
|                                              |                                                                                |
## Further reading

- [Libiry2Go for developers](Libiry2Go%20for%20developers.md) 
- [Output format](Libiry2Go%20output%20format.md) - Understanding the generated files
