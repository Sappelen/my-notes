---
title: Libiry2Go usage guide
---

## System Requirements

- Python 3.12
- Same dependencies as Libiry
- Installed with Libiry (no separate installation)

## GUI Mode

### Starting the GUI

**Windows:**
```batch
Libiry2Go.bat
```

**Other platforms:**
```bash
python libiry2go.py
```

### GUI Workflow

1. **Select Source Folder**
   - Click "Browse" next to "Source folder"
   - Navigate to your ebook library
   - Click "Select Folder"

2. **Select Output Folder**
   - Click "Browse" next to "Output folder"
   - Choose where to save the markdown files
   - Default: creates folder next to source

3. **Configure Options**
   - **Books per file**: 1 for Obsidian, 50-100 for batched output
   - Format is determined by books per file setting

4. **Generate**
   - Click "Generate"
   - Progress is shown in the status area
   - Files are created in the output folder

## Command Line Mode

### Basic Syntax

```bash
python libiry2go.py [source] [output] [books_per_file]
```

### Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `source` | Yes | Path to ebook library folder |
| `output` | No | Output folder (default: next to source) |
| `books_per_file` | No | Books per file (default: 100) |

### Examples

```bash
# Scan C:\Books, output to C:\Books_catalog
python libiry2go.py "C:\Books"

# Scan with custom output location
python libiry2go.py "C:\Books" "D:\Catalogs\MyBooks"

# One file per book (Obsidian format)
python libiry2go.py "C:\Books" "D:\Obsidian\Books" 1

# 25 books per file
python libiry2go.py "C:\Books" "D:\Catalogs" 25

# 100 books per file (default)
python libiry2go.py "C:\Books" "D:\Catalogs" 100
```

### Headless/Batch Usage

Perfect for automation:

```batch
@echo off
REM Weekly catalog update
python libiry2go.py "C:\Books" "D:\Backup\catalog" 100
```

## Output Structure

### Multiple Books Per File (books_per_file > 1)

```
Output/
├── libiry2go_2026-02-13_part1.md
├── libiry2go_2026-02-13_part2.md
└── libiry2go_2026-02-13_part3.md
```

Filename format: `libiry2go_YYYY-MM-DD_partN.md`

### One File Per Book (books_per_file = 1)

```
Output/
├── The-Lord-of-the-Rings.md
├── Dune.md
├── Foundation.md
└── ...
```

Filename derived from book title (sanitized for filesystem).

## Processing Details

### Scanned Formats

| Format | Metadata | Cover |
|--------|----------|-------|
| EPUB | Full | Yes |
| MOBI/AZW | Full | Yes |
| PDF | Full | Yes |
| CBR/CBZ | Basic | Yes |
| Markdown | Full | Yes |
| Other files | Filename only | No |

### Recursive Scanning

- Scans all subfolders
- Preserves folder structure in metadata (path field)
- Skips hidden files and folders

### Field Mapping

Uses the same field names configured in Libiry's `customize.txt`:

```ini
Field name cover: cover
Field name booktitle: booktitle
Field name author: author
```

This ensures consistency across all Libiry ecosystem tools.

## Performance

| Library Size | Approximate Time |
|--------------|------------------|
| 100 books | ~10 seconds |
| 1,000 books | ~1 minute |
| 10,000 books | ~10 minutes |

Times vary based on:
- File format complexity
- Storage speed (SSD vs HDD)
- Cover extraction settings

## Tips

### For Obsidian Users

Use one file per book mode:
```bash
python libiry2go.py "C:\Books" "D:\Obsidian\Books" 1
```

Files will have YAML frontmatter compatible with:
- Book Search plugin
- Booksidian plugin
- Dataview queries

### For Mobile Sync

1. Generate catalog with Libiry2Go
2. Sync output folder to mobile (Dropbox, OneDrive, etc.)
3. View with any markdown app

### For Regular Updates

Create a batch script to refresh your catalog:

```batch
@echo off
python libiry2go.py "C:\Books" "C:\Catalog" 100
echo Catalog updated!
```
