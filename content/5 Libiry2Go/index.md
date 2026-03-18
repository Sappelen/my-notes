---
title: 5. Libiry2Go
---

Libiry2Go scans your library and creates markdown files containing book metadata. Perfect for creating mobile-friendly book lists, Obsidian vaults or backup catalogs. These files can be:
- Viewed on any device with a markdown reader
- Imported into Obsidian
- Used as a portable backup of your library catalog
- Shared with others as a reading list

## Key Features

- **Recursive scanning** - Processes entire folder hierarchies
- **Multiple formats** - Supports EPUB, MOBI, PDF, CBR, CBZ, and more
- **Two output modes** - One file per book or multiple books per file
- **Field compatibility** - Uses same field names as Libiry
- **Offline operation** - No internet required

## Quick Start

### Windows GUI

1. Run `Libiry2Go.bat`
2. Select your book folder
3. Choose an output location
4. Click Generate

### Command Line

```bash
# 50 books per file
python libiry2go.py "C:\Books" "C:\Output" 50
```

## Documentation

- [Usage Guide](Libiry2Go%20usage%20guide.md) - Detailed CLI and GUI instructions
- [Output Formats](Libiry2Go%20output%20formats.md) - Understanding the generated files

## When to Use Libiry2Go

| Scenario                           | Use Libiry2Go?                        |
| ---------------------------------- | ------------------------------------- |
| Create book library for mobile use | Yes                                   |
| Create Obsidian book vault         | Yes; choose One file per book           |
| Backup library metadata            | Yes                                   |
| Share reading list                 | Yes                                   |
| Browse books visually              | No; use complete book library instead |
| Edit book metadata                 | No; use complete book library instead |
