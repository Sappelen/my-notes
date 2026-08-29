---
title: 7 Developer guide
---
Technical documentation for developers working with or contributing to the Libiry ecosystem.

## Overview

The Libiry ecosystem consists of four main components:

| Component               | Language    | Framework | Purpose             |
| ----------------------- | ----------- | --------- | ------------------- |
| Libiry                  | Python 3.12 | Kivy      | Desktop application |
| Calibre2Libiry          | Python 3.12 | Kivy      | Renaming function   |
| Libiry2Go               | Python 3.12 | Kivy      | Catalog generator   |
| Libiry BookSpineScanner | JavaScript  | Vite/PWA  | Web-based scanner   |
and some [[Utilities]].

Installing Libiry on Windows for developers:  
git clone [https://github.com/sappelen/Libiry.git](https://github.com/sappelen/Libiry.git) "C:\Program Files\Libiry"  
cd "C:\Program Files\Libiry"  
.\install.bat  
.\Libiry.bat  
To create a desktop shortcut, right-click Libiry.bat → Send to → Desktop (create shortcut).  
Alternatively, use %LOCALAPPDATA%\Programs instead of C:\Program Files (no admin rights needed).  

Installing Libiry on Linux
Method 3 (for developers):  
git clone [https://github.com/sappelen/Libiry.git](https://github.com/sappelen/Libiry.git)  
cd Libiry  
chmod +x linux/install.sh  
sudo linux/install.sh  
libiry  

Libiry will be installed in folder /opt/Libiry
  
## Documentation

- [[content/7 For developers/Architecture]] 
- [[Contributing to Libiry]]
- [[Libiry roadmap]]

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

## Key technologies

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

## Testing

### Launch options for Libiry!!!

| Windows          | Or directly    | Description                              | Use Case        |
| ---------------- | -------------- | ---------------------------------------- | --------------- |
| libiry.bat       |                | Silent launch (pythonw.exe)              | Normal use      |
| libiry_debug.bat | python main.py | With console output                      | Troubleshooting |
| libiry.sh        |                | Via the shell script (output is visible) |                 |
 STEP 3 — RUN LIBIRY
-----------------------------------------------------------------------

Double-click run.bat to start the main Libiry application.
Double-click Libiry2Go.bat to start the catalog generator.
Double-click Calibre2Libiry.bat to start the Calibre converter.
Double-click Align_book_data.bat to start the book data tool
  
  /opt/Libiry/venv/bin/python /opt/Libiry/main.py

  Or via the shell script (output also visible):
  /opt/Libiry/Libiry.sh

  The full Python path gives the clearest debug output — all print() statements and tracebacks appear directly in the terminal.

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

1. UI is defined in main.py using Kivy widgets
2. Colors/fonts configured in customize.txt
3. Grid rendering in app/grid_widget.py

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
