---
title: 6. Developer guide
---
Technical documentation for developers working with or contributing to the Libiry ecosystem.

## Overview

The Libiry ecosystem consists of four main components:

| Component | Language | Framework | Purpose |
|-----------|----------|-----------|---------|
| Libiry | Python 3.12 | Kivy | Desktop application |
| Calibre2Libiry | Python 3.12 | tkinter | Renaming function |
| Libiry2Go | Python 3.12 | tkinter | Catalog generator |
| Libiry BookSpineScanner | JavaScript | Vite/PWA | Web-based scanner |

and some [[Utilities]].

## Documentation

- [[Architecture]] 
- [[Contributing to Libiry]]

## Quick start for developers

### Setting up a Libiry development environment

```bash
# Clone repository
git clone https://github.com/sappelen/Libiry.git
cd Libiry

# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run in debug mode
python main.py
```

### Setting up a Libiry BookSpineScanner development environment

```bash
# Navigate to folder
cd BookSpineScanner

# Install dependencies
npm install

# Start dev server
npm run dev

# Build for production
npm run build
```

## Code structure

### Libiry (Python)

```
Libiry/
├── main.py              # Main application (5000+ lines)
├── libiry2go.py         # Catalog generator
├── app/
│   └── grid_widget.py   # RecycleView grid component
├── core/
│   ├── metadata_extractor.py  # Metadata from all formats
│   ├── cover_extractor.py     # Cover image extraction
│   ├── cover_cache.py         # SQLite thumbnail cache
│   ├── file_opener.py         # Open files in apps
│   └── library.py             # Folder scanning
└── resources/
    └── icons/           # UI icons
```

### Libiry BookSpineScanner (JavaScript)

```
BookSpineScanner/
├── index.html           # Entry point
├── src/
│   ├── main.js          # Application logic
│   └── styles.css       # Styling
├── public/              # PWA assets
├── vite.config.js       # Build configuration
└── package.json         # Dependencies
```

## Key Technologies

### Libiry

- **Kivy** - Cross-platform UI (OpenGL-based)
- **RecycleView** - Efficient grid rendering
- **SQLite** - Thumbnail caching
- **PyMuPDF** - PDF processing
- **ebookmeta** - EPUB metadata
- **mobi** - MOBI file support
- **comicbox** - Comic book support
- **Pillow** - Image processing

### Libiry BookSpineScanner

- **Tesseract.js** - Client-side OCR
- **Vite** - Fast build tool
- **PWA** - Progressive Web App features
- **IndexedDB** - Local data caching

## API Reference

### metadata_extractor.py

```python
from core.metadata_extractor import extract_metadata

# Extract metadata from any supported format
metadata = extract_metadata(Path("book.epub"))
# Returns: dict with keys like 'title', 'author', 'tags', etc.

# OPF sidecar operations
from core.metadata_extractor import (
    read_opf_tags,
    write_opf_tags,
    modify_opf_tags,
    get_opf_path
)

# Read tags from OPF
tags = read_opf_tags(Path("book.mobi"))

# Write tags to OPF
success = write_opf_tags(Path("book.mobi"), ["fiction", "fantasy"])

# Modify existing tags
success = modify_opf_tags(
    Path("book.mobi"),
    tags_to_remove={"old-tag"},
    tag_to_add="new-tag"
)
```

### cover_extractor.py

```python
from core.cover_extractor import extract_cover

# Extract cover from ebook
cover_path = extract_cover(Path("book.epub"), Path("output/"))
# Returns: Path to extracted cover image or None
```

### cover_cache.py

```python
from core.cover_cache import CoverCache

# Initialize cache
cache = CoverCache()

# Get cached thumbnail
thumbnail = cache.get_thumbnail(Path("book.epub"))

# Cache a thumbnail
cache.set_thumbnail(Path("book.epub"), thumbnail_bytes)

# Clear cache
cache.clear()
```

## Testing

### Launch options for Libiry

| Windows | Or directly |Description | Use Case |
|--------|------|-------|----------|
| `run.bat` | |Silent launch (pythonw.exe) | Normal use |
| `run_debug.bat` |`python main.py`| With console output | Troubleshooting |
| `debug.bat` || Alternative debug mode | Development |

Debug output shows:
- File loading progress
- Metadata extraction results
- Error messages

### Libiry BookSpineScanner development

```bash
npm run dev
# Opens http://localhost:5173 with hot reload
```

## Common development tasks

### Adding a new file format

1. Add extension to `selected types.txt`
2. Create extraction function in `metadata_extractor.py`
3. Add cover extraction in `cover_extractor.py`
4. Handle in main.py display logic

### Modifying the UI

1. UI is defined in `main.py` using Kivy widgets
2. Colors/fonts configured in `customize.txt`
3. Grid rendering in `app/grid_widget.py`

### Adding new metadata fields

1. Add field to extraction functions
2. Update display in main.py
3. Add field mapping in customize.txt
4. Update Libiry2Go export

## Building

### Libiry for distribution

Libiry is distributed as source code. For packaging:

```bash
# PyInstaller (Windows)
pip install pyinstaller
pyinstaller --onefile --windowed main.py
```

### Libiry BookSpineScanner for production

```bash
npm run build
# Output in dist/ folder
# Deploy to GitHub Pages or any static host
```
