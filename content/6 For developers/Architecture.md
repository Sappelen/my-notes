---
title: Architecture
---

Detailed technical documentation of the Libiry ecosystem architecture.

## System Overview

```
┌───────────────────────────────────────────────────────────────────┐
│                        Libiry Ecosystem                           │
├───────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌───────────────┐  ┌───────────────┐  ┌───────────────────────┐  │
│  │    Libiry     │  │  Libiry2Go    │  │   BookSpineScanner    │  │
│  │   (Desktop)   │  │   (CLI/GUI)   │  │       (PWA)           │  │
│  │               │  │               │  │                       │  │
│  │  ┌─────────┐  │  │  ┌─────────┐  │  │  ┌───────────────┐    │  │
│  │  │  Kivy   │  │  │  │ tkinter │  │  │  │ Tesseract.js  │    │  │
│  │  │   UI    │  │  │  │   GUI   │  │  │  │    or GCV     │    │  │
│  │  └────┬────┘  │  │  └────┬────┘  │  │  └───────┬───────┘    │  │
│  │       │       │  │       │       │  │          │            │  │
│  │  ┌────┴────┐  │  │       │       │  │  ┌───────┴───────┐    │  │
│  │  │  Core   │◄─┼──┼───────┘       │  │  │   Book APIs   │    │  │
│  │  │ Modules │  │  │               │  │  └───────────────┘    │  │
│  │  └─────────┘  │  │               │  │                       │  │
│  └───────────────┘  └───────────────┘  └───────────────────_───┘  │
│           │                                         │             │
│           ▼                                         ▼             │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │                    File System                              │  │
│  │  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐ ┌──────────┐  │  │
│  │  │ EPUB │ │ MOBI │ │ PDF  │ │ CBZ  │ │ CBR  │ │ Markdown │  │  │
│  │  └──────┘ └──────┘ └──────┘ └──────┘ └──────┘ └──────────┘  │  │
│  │                         │                                   │  │
│  │  ┌────────────────────────┴──────────────────────────────┐  │  │
│  │  │              OPF sidecar (buddy) files                │  │  │
│  │  │    (for MOBI, AZW, CBR, problematic PDFs)             │  │  │
│  │  └───────────────────────────────────────────────────────┘  │  │
│  └─────────────────────────────────────────────────────────────┘  │
└───────────────────────────────────────────────────────────────────┘
```

## Libiry Desktop Application

### Application Structure

```
┌────────────────────────────────────────────────────────────┐
│                      main.py                               │
│  ┌────────────────────────────────────────────────────┐    │
│  │                   LibiryApp                        │    │
│  │  ┌────────────┐  ┌────────────┐  ┌──────────────┐  │    │
│  │  │  Settings  │  │   Grid     │  │   Status     │  │    │
│  │  │   Panel    │  │   View     │  │    Bar       │  │    │
│  │  └────────────┘  └────────────┘  └──────────────┘  │    │
│  └────────────────────────────────────────────────────┘    │
│                           │                                │
│  ┌────────────────────────┴────────────────────────────┐   │
│  │                  Core Modules                       │   │
│  │  ┌──────────────────┐  ┌──────────────────────────┐ │   │
│  │  │metadata_extractor│  │    cover_extractor       │ │   │
│  │  └──────────────────┘  └──────────────────────────┘ │   │
│  │  ┌──────────────────┐  ┌──────────────────────────┐ │   │
│  │  │   cover_cache    │  │     file_opener          │ │   │
│  │  └──────────────────┘  └──────────────────────────┘ │   │
│  │  ┌──────────────────┐                               │   │
│  │  │     library      │                               │   │
│  │  └──────────────────┘                               │   │
│  └─────────────────────────────────────────────────────┘   │
└────────────────────────────────────────────────────────────┘
```

### Key Classes

#### LibiryApp (main.py)

Main Kivy application class:
- Initializes UI components
- Handles navigation and state
- Manages settings persistence
- Coordinates background operations

```python
class LibiryApp(App):
    def build(self):
        # Create main layout
        # Initialize grid view
        # Set up event handlers
        pass
```

#### GridWidget (app/grid_widget.py)

Kivy RecycleView-based grid for displaying books:
- Efficient rendering for large collections
- Dynamic tile sizing
- Selection handling
- Lazy loading of covers

```python
class GridWidget(RecycleView):
    def __init__(self):
        # Configure RecycleView
        # Set up selection behavior
        pass
```

### Core Modules

#### metadata_extractor.py

Central metadata handling:

```python
def extract_metadata(path: Path) -> dict:
    """Extract metadata from any supported file type."""
    ext = path.suffix.lower()
    if ext == '.epub':
        return _extract_epub(path)
    elif ext in ('.mobi', '.azw', '.azw3'):
        return _extract_mobi(path)
    # ... etc
```

Format-specific extractors:
- `_extract_epub()` - Uses ebookmeta
- `_extract_mobi()` - Uses mobi library
- `_extract_pdf()` - Uses PyMuPDF
- `_extract_comic()` - Uses comicbox
- `_extract_markdown()` - Custom parser

OPF sidecar functions:
- `get_opf_path()` - Generate OPF path for any file
- `read_opf_tags()` - Parse OPF XML for tags
- `write_opf_tags()` - Create/update OPF with tags
- `modify_opf_tags()` - Add/remove specific tags

#### cover_extractor.py

Cover image extraction:

```python
def extract_cover(path: Path, output_dir: Path) -> Optional[Path]:
    """Extract cover from ebook, return path to image."""
    pass
```

Supports:
- EPUB cover images
- MOBI cover records
- PDF first page rendering
- Comic first image

#### cover_cache.py

SQLite-backed thumbnail caching:

```python
class CoverCache:
    def __init__(self, cache_dir: Path = None):
        # Initialize SQLite database
        pass

    def get_thumbnail(self, path: Path) -> Optional[bytes]:
        # Return cached thumbnail or None
        pass

    def set_thumbnail(self, path: Path, data: bytes):
        # Store thumbnail in cache
        pass
```

Cache location: `~/.libiry/cache/`

Cache structure:
  _file_cache = {
      "path/to/file.md": {
          "tags": ["tag1", "tag2"],
          "is_multibook": True,
          "book_count": 3,
          "mtime": 1234567890.0  # for invalidation
          }
	  }
### Data Flow

#### Book display flow

```
1. User navigates to folder
        │
        ▼
2. Scan folder for supported files
        │
        ▼
3. For each file:
   ├── Check cover cache
   │   ├── Hit: Use cached thumbnail
   │   └── Miss: Extract cover
   │           ├── Save to cache
   │           └── Generate thumbnail
   ├── Extract metadata
   │   ├── Check for OPF sidecar
   │   └── Read from file
   └── Create grid tile
        │
        ▼
4. Display in RecycleView grid
```

#### Tag editing flow

```
1. User selects books
        │
        ▼
2. Edit button → User edits metadata
        │
        ▼
3. For each selected file:
   ├── Determine storage method:
   │   ├── EPUB: Write to ebook
   │   ├── MOBI/AZW: Write to OPF
   │   ├── CBZ: Write to ComicInfo.xml
   │   ├── CBR: Write to OPF
   │   ├── PDF: Try ebook, fallback to OPF
   │   └── Markdown: Write to file
   └── Update file
        │
        ▼
4. Refresh display
```

## Libiry2Go Architecture

```
┌────────────────────────────────────────┐
│              libiry2go.py              │
│  ┌──────────────────────────────────┐  │
│  │         Main Application         │  │
│  │  ┌────────────┐  ┌────────────┐  │  │
│  │  │    GUI     │  │    CLI     │  │  │
│  │  │  (tkinter) │  │  (argparse)│  │  │
│  │  └─────┬──────┘  └──────┬─────┘  │  │
│  │        └────────┬───────┘        │  │
│  │                 ▼                │  │
│  │  ┌──────────────────────────────┐│  │
│  │  │      Library Scanner         ││  │
│  │  │(uses core.metadata_extractor)││  |
│  │  └──────────────────────────────┘│  │
│  │                 │                │  │
│  │                 ▼                │  │
│  │  ┌──────────────────────────────┐│  │
│  │  │     Markdown Generator       ││  │
│  │  │  ├── YAML format             ││  │
│  │  │  └── Flat format             ││  │
│  │  └──────────────────────────────┘│  │
│  └──────────────────────────────────┘  │
└────────────────────────────────────────┘
```

## BookSpineScanner architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    BookSpineScanner (PWA)                   │
│  ┌─────────────────────────────────────────────────_────┐   │
│  │                     main.js                          │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐   │   │
│  │  │   Camera    │  │     OCR     │  │    Book     │   │   │
│  │  │   Module    │  │    Module   │  │   Lookup    │   │   │
│  │  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘   │   │
│  │         │                │                │          │   │
│  │         ▼                ▼                ▼          │   │
│  │  ┌───────────────────────────────────────────────┐   │   │
│  │  │              Result Manager                   │   │   │
│  │  │  ├── Confidence scoring                       │   │   │
│  │  │  ├── User corrections                         │   │   │
│  │  │  └── Export generation                        │   │   │
│  │  └───────────────────────────────────────────────┘   │   │
│  └──────────────────────────────────────────────────────┘   │
│                            │                                │
│  ┌─────────────────────────┴──────────────────────────┐     │
│  │                  External APIs                     │     │
│  │  ┌────────────┐ ┌────────────┐ ┌───────────────┐   │     │
│  │  │Open Library│ │Google Books│ │  Europeana    │   │     │
│  │  └────────────┘ └────────────┘ └───────────────┘   │     │
│  └────────────────────────────────────────────────────┘     │
└─────────────────────────────────────────────────────────────┘
```

### OCR Pipeline

```
Photo Capture
     │
     ▼
Spine Detection (OpenCV.js)
     │
     ├── Detect rectangles
     ├── Filter by aspect ratio
     └── Extract spine regions
     │
     ▼
OCR Processing
     │
     ├── Tesseract.js (offline)
     │   └── Character recognition
     │
     └── Google Cloud Vision (online)
         └── Document text detection
     │
     ▼
Text Cleanup
     │
     ├── Remove noise
     ├── Identify title/author patterns
     └── Extract ISBN if present
     │
     ▼
Book Lookup
     │
     ├── Search Open Library
     ├── Search Google Books
     └── Search Europeana
     └── Search Library of Congress
     │
     ▼
Confidence Scoring
     │
     ├── High (>85%): Green
     ├── Medium (50-85%): Orange
     └── Low (<50%): Red
```

## Data Formats

### OPF Sidecar Format

```xml
<?xml version="1.0" encoding="UTF-8"?>
<package xmlns="http://www.idpf.org/2007/opf" version="3.0">
  <metadata xmlns:dc="http://purl.org/dc/elements/1.1/">
    <dc:subject>tag1</dc:subject>
    <dc:subject>tag2</dc:subject>
  </metadata>
</package>
```

### Markdown YAML Format

```yaml
---
cover: "url"
booktitle: "Title"
author: "Author"
isbn: "ISBN"
tags: [tag1, tag2]
rating: 8
---
```

### Markdown Flat Format

The minimum requirement is a cover line. In it, you can put author plus title. You can create files like this completely by hand, if you want to:
```
cover: author 1 - title 1
cover: author 1 - title 2
cover: author 2 - title 3
cover: author 3 - title 4
cover: author 4 - title 5
```
etcetera.

The LibiryBookSpineSpanner produces structured files like this:
```
cover: url
booktitle: Title
author: Author
tags: tag1, tag2
```


## Performance Considerations

### Lazy Loading

- Grid only renders visible tiles
- Covers loaded on demand
- Metadata extracted as needed

### Caching Strategy

- SQLite for thumbnails
- In-memory for current folder
- No caching of raw metadata

### Background Threading

- Folder scans run in background
- UI remains responsive
- Progress updates via Kivy Clock

## Security

### File Access

- Read/write only to user-specified folders
- No network access except for cover lookup
- No data collection or telemetry

### Libiry BookSpineScanner

- All processing happens in the browser or app
- Photos are never uploaded
- Settings are stored in local storage only
- API calls are only used for metadata lookup
