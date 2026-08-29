---
title: Libiry2Go usage guide
---
## System Requirements

- Python 3.12
- Same dependencies as Libiry
- Installed together with Libiry

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

## Command line mode

### Basic syntax

```bash
python libiry2go.py [source] [output]
```

### Parameters

| Parameter | Required | Description                             |
|-----------|----------|-------------|
| `source` | Yes | Path to e-book library folder           |
| `output` | No | Output folder (default: next to source) |
### Examples

```bash
# Scan C:\Books, output to C:\Books\Libiry2Go_Output
python libiry2go.py "C:\Books"

# Scan with custom output location
python libiry2go.py "C:\Books" "D:\Catalogs\MyBooks"
```
### Headless/batch usage

Perfect for automation:

```batch
@echo off
REM Weekly catalog update
python libiry2go.py "C:\Books" "D:\Backup\catalog"
```

or

```batch
@echo off
python libiry2go.py "C:\Books" "C:\Catalog" 
echo Catalog updated!
```

## Processing details

### Scanning

- All subfolders are included
- Preserves folder structure in metadata (path field)
- Skips hidden files and folders
- Supported file types are exactly the same as in Libiry

### Field mapping

Uses the custom field names that you set in Libiry:

```ini
Field name cover: cover
Field name booktitle: booktitle
Field name author: author
...
etcetera
```

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
