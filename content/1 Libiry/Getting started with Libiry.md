---
title: Getting started with Libiry
---

This guide will help you get up and running with Libiry quickly.

### For displaying your ebooks (EPUB, PDF, MOBI, etc.)

1. **Install Libiry** - [Installation Guide](Libiry%20installation%20guide.md)
2. **Point it to your library** - Set your ebook folder location in Settings
3. **Start browsing** - View covers, search, filter by tags

→ [Continue to Libiry Installation](Libiry%20installation%20guide.md)

### For displaying the physical books you have on shelves

1. **Open the [Libiry BookspineScanner](https://sappelen.github.io/BookSpineScanner).
2. **Take photos** of your bookshelves
3. **Review & export** the book scans to markdown files
4. **Open the markdown files in Libiry

Alternatively, you can create markdown files by hand with one line for every book on your book shelf.
In it, you store either a URL to the cover or the book title.

→ [Continue to BookSpineScanner Guide](2%20Libiry%20Bookspinescanner/index.md)

### For a portable catalog of your collection

1. **Install Libiry2Go**, it's included with Libiry
2. **Run the generator** and point it to your ebook folder
3. **Get markdown files** that are perfect for Obsidian or for mobile viewing

→ [Continue to Libiry2Go Guide](4%20Libiry2Go/index.md)

## Install Libiry

### Windows

1. Download the latest release from [GitHub](https://github.com/sappelen/Libiry/releases)
2. Extract to a folder (e.g., `C:\Libiry`)
3. Run `install.bat` to set up the virtual environment
4. Run `run.bat` to start Libiry

### Requirements

- **Python 3.12** (Kivy doesn't support 3.14 yet)
- **Windows/Linux/macOS** for desktop
- **Modern browser** for BookSpineScanner (Chrome, Firefox, Safari)

### Limitations

- Does not read existing metadata for MOBI, AZW, CBR and for some problematic PDFs
- Only reads existing OPF files that have the same name and folder as the book itself (f.e. book.pdf.opf for a book named book.pdf)
- No validation for maintaining metadata like ISBN numbers
## First launch

When you first open Libiry:

1. Click the **Settings** button (gear icon)
2. Set your **Library location** - the folder containing your ebooks
3. Click **Save**
4. Your books will now appear as a grid of covers

## Next steps

- [Learn about Features](Libiry%20features.md)
- [Configure Libiry](Customizing%20Libiry.md)
- [Keyboard Shortcuts](Keyboard%20shortcuts.md)
- [Troubleshooting](Troubleshooting.md)
