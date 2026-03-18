---
title: Utilities
---

Libiry includes several standalone utility scripts for maintenance and troubleshooting.

## Available utilities

| Utility                                     | Purpose                                  | Documentation                                    |
| ------------------------------------------- | ---------------------------------------- | ------------------------------------------------ |
| [check_pdf_tags.py](PDF%20Tag%20Checker.md) | Identify PDFs with tag read/write issues | [Guide](PDF%20Tag%20Checker.md)                  |
| create_icons.py                             | Generate application icons               | Internal use                                     |
| install.bat                                 | Install dependencies                     | [Installation](Libiry%20installation%20guide.md) |

## PDF Tag Checker

The most commonly used utility. Scans your library to identify PDFs that cannot store tags directly, and creates OPF sidecar files for them in bulk. It is there for performance purposes only. You can use Libiry without using the PDF Tag Checker.

**Quick usage:**
```bash
python check_pdf_tags.py "C:\Books"
```

[Full documentation →](PDF%20Tag%20Checker.md)

## Batch scripts

### Windows launchers

| Script | Purpose |
|--------|---------|
| `run.bat` | Launch Libiry (no console) |
| `run_debug.bat` | Launch Libiry with console output |
| `debug.bat` | Alternative debug launcher |
| `install.bat` | Create venv and install dependencies |
| `Libiry2Go.bat` | Launch Libiry2Go |
### Usage

All batch scripts should be run from the Libiry folder:

```batch
cd C:\path\to\Libiry
run.bat
```

## Creating custom scripts

### Python Environment

Use the Libiry virtual environment:

```batch
@echo off
cd /d "%~dp0"
call venv\Scripts\activate
python your_script.py
```

### Importing Libiry modules

Your custom scripts can use Libiry's core modules:

```python
import sys
from pathlib import Path

# Add Libiry to path
sys.path.insert(0, str(Path(__file__).parent))

# Import modules
from core.metadata_extractor import extract_metadata
from core.cover_extractor import extract_cover

# Use them
metadata = extract_metadata(Path("book.epub"))
print(metadata)
```

### Available modules

| Module | Functions |
|--------|-----------|
| `core.metadata_extractor` | `extract_metadata()`, OPF helpers |
| `core.cover_extractor` | `extract_cover()` |
| `core.cover_cache` | Thumbnail caching |
| `core.file_opener` | Open files in apps |
| `core.library` | Folder scanning |

## Automation examples

### Weekly catalog update

```batch
@echo off
REM update_catalog.bat - Run weekly via Task Scheduler

cd /d "C:\Libiry"
call venv\Scripts\activate

REM Generate updated catalog
python libiry2go.py "D:\Books" "D:\Catalog" 100

REM Check for problematic PDFs
python check_pdf_tags.py "D:\Books"

echo Done!
```

### Scan new PDFs

```batch
@echo off
REM scan_new_pdfs.bat - Check only recent PDFs

cd /d "C:\Libiry"
call venv\Scripts\activate

python check_pdf_tags.py "D:\Books\NewArrivals"
```
