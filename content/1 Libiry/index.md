---
title: 1. Libiry
---
Libiry is a cross-platform desktop application for browsing and managing your book library. It provides a simple visual overview of all your books - analog, digital, and audio.
Libiry is self-hosted. Your books and data remain on your desktop or mobile device, without any subscription fees or cloud dependency. You can place your book library in a cloud folder of your choice if you wish.
Libiry is free and open source. 

![[https://sappelen.com/wp-content/uploads/2026/03/Libiry-grid-800x421.png]]

## Key Features

- **Simple** - No frills
- **Visual grid display** - See all your books in a cover grid
- **No database required** - Works directly on your existing folder structure
- **Cross-platform** - Windows, Linux, macOS, Android, iOS
- **Offline support** - Works without an internet connection
- **Privacy-focused** - No accounts, no tracking, no cloud dependency
- **Fully customizable** - Colors, fonts, field names
- **Bulk tag management** - Add, edit, and filter by tags
- **Metadata management** - Maintain title, author, ISBN etcetera
- **Duplicate detection** - Find duplicate books
- **Search** - with optional fuzzy matching
- **Format agnostic** - Supports EPUB, MOBI, PDF, CBR, CBZ, Markdown, MP3 and more
- **Works with Goodreads, Obsidian and Calibre** - Import/export with Goodreads CSV format, files compatible with Obsidian (and its plugins), works on Calibre library

## Workflow tips

## Documentation

### Setup
- [Installation Guide](Libiry%20installation%20guide.md) - How to install Libiry
- [Configuration](Customizing%20Libiry.md) - Customize colors, fonts, and behavior

### Using Libiry
- [Features Overview](Libiry%20features.md) - All features explained
- [User Interface Guide](User%20interface.md) - Understanding the UI
- [Keyboard Shortcuts](Keyboard%20shortcuts.md) - Quick reference

### Technical
- [Supported file formats](Supported%20file%20formats.md) - EPUB, PDF, MOBI, and more
- [Metadata handling](Metadata%20handling.md) - How metadata is extracted and stored
- [Troubleshooting](Troubleshooting.md) - Common issues and solutions

## Screenshots

### Main View
The main grid view displays book covers with optional title and tag overlays.

### Settings Panel
Customize colors, fonts, scrollbar appearance, and more.

### Tag Filter
Click any tag in the status bar at the bottom to filter by that tag.

## System Requirements

| Platform | Requirements |
|----------|--------------|
| Windows | Windows 10/11, Python 3.12 |
| Linux | Ubuntu 20.04+, Python 3.12 |
| macOS | macOS 11+, Python 3.12 |
| Android | Android 8.0+ (via Buildozer) |
| iOS | iOS 13+ (via Kivy-iOS) |

## Quick start

```bash
# Clone the repository
git clone https://github.com/sappelen/Libiry.git

# Navigate to folder
cd Libiry

# Install dependencies (Windows)
install.bat

# Run (Windows)
run.bat
```

## Architecture

Libiry is built with:
- **[Kivy](https://kivy.org/)** - Cross-platform UI framework
- **Python 3.12** - Core application logic
- **SQLite** - Thumbnail caching (local only)
- **PyMuPDF/ebookmeta/mobi** - Ebook metadata extraction
