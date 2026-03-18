---
title: 2. Libiry BookSpineScanner
---
The Libiry BookSpineScanner is a Progressive Web App (PWA) that identifies books with spine OCR and barcode detection. It gives you flat markdown files that can be used in Libiry, Obsidian and other tools.

![[https://marjonw.wordpress.com/wp-content/uploads/2026/03/bookspinescanner.png]]

## How it works

1. Open the [BookSpineScanner](https://sappelen.github.io/BookSpineScanner/)
2. Check the settings. Which OCR Engine do you want to use?
3. Take a photo of your bookshelf (or upload a photo)
4. The tool detects individual book spines
5. The tool uses [OCR](OCR%20engines%20used%20in%20the%20Libiry%20BookSpineScanner.md) to extract text from each spine
6. The tools looks up books in various online databases
7. Review the results and correct mistakes
8. Export the results to markdown files
9. Open the markdown files in Libiry or in another tool

### 7. Review the results and correct mistakes

Confidence indicators:
- 🟢 **Green** - correct match (>85% confidence that the OCR text matches this book in the database)
- 🟠 **Orange** - uncertain match (50-85% confidence)
- 🔴 **Red** - incorrect match (<50% confidence)

Expand each detected book to show preliminary title, title, author, cover image etcetera (if found).

Before exporting, review each detected book. Fix or delete wrong matches and add missing books. Manually add tags to individual books.
Toggle the colored dot to change the color.
For red books the preliminary book title is exported instead of the matched book title. 

### 8. Export the results to markdown files

Before exporting, add common tags like:
- analog (physical book)
- shelf/bottomleft (location)
- genre/scifi (genre)
- status/to-read (reading status)
to all your books by putting them in the tag box at the bottom of the screen.

You can export one or more markdown files or you can choose to download a ZIP file.

Keep your scan photos until you've verified the export. If you find errors later, you can re-scan.

## Key features

- **Spine OCR** - Reads text from book spines
- **Barcode Scanning** - Detects ISBN barcodes
- **Multiple OCR Engines** - Tesseract.js (offline) or Google Cloud Vision
- **Book Lookup** - Searches Open Library, Google Books, Europeana, Library of Congress
- **Confidence Indicators** - Shows match quality for each book
- **Export to Markdown** - Compatible with Libiry and Obsidian
- **Works Offline** - After initial load, Tesseract.js works without internet
- **Installable** - Add to home screen on mobile devices

## Barcode mode

For books with a visible ISBN barcode:

- Enable "Barcode mode" in Settings
- Take a photo of the barcodes
- The app reads ISBN numbers directly from the barcodes
- Books are looked up by ISBN in Open Library, Google Books, Europeana and Library of Congress
- If a book is not found in these databases, a WorldCat search link is provided as the book title -- click it to look up the book manually

## Supported platforms

| Platform | Browser         | Installation       |
| -------- | --------------- | ------------------ |
| Android  | Chrome, Firefox | Add to home screen |
| iOS      | Safari          | Add to home screen |
| Windows  | Chrome, Edge    | Install as app     |
| macOS    | Chrome, Safari  | Install as app     |
| Linux    | Chrome, Firefox | Install as app     |
## Privacy

- **All processing happens in your browser** - Photos never leave your device
- **No accounts required** - No sign-up, no tracking
- **Local storage only** - Settings are saved in your browser only
- **API calls** - Only for book metadata lookup (Open Library etc.)

## Comparison with manual cataloging

| Method                  | Time per Book | Accuracy | Best For          |
| ----------------------- | ------------- | -------- | ----------------- |
| Libiry BookSpineScanner | ~5 seconds    | 70-90%   | Large collections |
| ISBN scanner            | ~30 seconds   | 99%      | Small batches     |
| Manual entry            | ~2 minutes    | 100%     | Single books      |
|                         |               |          |                   |

The Libiry BookSpineScanner works best when:
- You have many books to catalog
- Books have readable spines
- You can verify and correct matches

- Spine text must be readable (not too small/faded)
- Old/damaged books may not OCR well
- Matching depends on book being in online databases
- Some manual correction are usually needed
### Install as an app (optional)

- **Android (Chrome):** Tap the three-dot menu > "Install app" or "Add to home screen"
- **iPhone (Safari):** Tap the share icon (square with arrow) > "Add to home screen"
- **Desktop (Chrome/Edge):** Click the install icon in the address bar

## OCR engines

### Tesseract.js (default)

- Works offline, no setup required
- Runs entirely in your browser
- Good for high-contrast, well-lit photos

### Google Cloud Vision (recommended)

- Much better results, especially for book spines with small or rotated text
- Requires a Google Cloud Vision API key
- Free tier: 1,000 scans/month, then approximately $1.50 per 1,000 scans

**To set up Google Cloud Vision:**- Go to [Google Cloud Console](https://console.cloud.google.com/)
- Create a project (or select an existing one)
- Enable the "Cloud Vision API"
- Go to "Credentials" and create an API key
- In BookSpineScanner, tap the gear icon (Settings)
- Paste your API key in the "Google Vision API Key" field
- Select "Google Cloud Vision" as OCR engine

## Book databases

### Google Books
### Europeana

- Best for historical/European works
- Get a free key at [pro.europeana.eu](https://pro.europeana.eu/page/get-api)
### Library of Congress
   
- Best for U.S.-published books, especially academic, nonfiction, and trade books
## Export formats

### One file per photo (default)

- YAML header with scan metadata
- Each book as a block with 'key: value' lines
- Compatible with Libiry, readable in any other text editor or reader

### One file per book

- One '.md' file per book
- All metadata in YAML frontmatter
- Compatible with Obsidian, Logseq, Calibre, Libiry and any other text editor or reader
- Download as ZIP when exporting multiple books

## Customizing options

Edit file 'customize/customize.txt' to change the app's appearance.  
If your existing Obsidian or Libiry setup uses different field names, you can configure them in Settings.

## Data and privacy

- All processing happens in your browser. No data is sent to any server (except API calls to Google Vision, Open Library and Google Books when looking up books)
- Settings are stored in your browser's localStorage
- Book lookup results are cached in IndexedDB to reduce API calls
- No account required, no tracking, no analytics

## Integration with Libiry

- Place the markdown files in your Libiry book folder
- Refresh Libiry

Libiry reads the book metadata fields 'cover', 'booktitle', 'author', 'isbn', 'publisher', 'year', 'language' and 'tags' from the markdown files.  
Other fields are ignored by Libiry but preserved in the file.

**Note:** Libiry supports a maximum of 100 books per markdown file for performance reasons. If a scan contains more than 100 books, BookSpineScanner automatically splits the export into multiple files (`shelf_part1.md`, `shelf_part2.md`, etc.).
## Further reading

- [Scanning guide](Scanning.md) - How to take good photos and scan books
- [Export options](Libiry%20BookSpineScanner%20export.md) - Output formats and Obsidian integration
