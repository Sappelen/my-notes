---
title: 2 Libiry BookSpineScanner
---
![[libiry-bookspinescanner.png]]

Taking stock of your analog books is not a big project anymore. It can easily be done in parts, too.
With the Libiry BookspineScanner you can add your physical books to your book collection overview with only one photo per book shelf. 

## Key features

- **Spine [OCR](8%20Glossary/OCR)** - Reads text from book spines
- **Barcode scanning** - Detects ISBN barcodes
- **Multiple OCR engines** - Tesseract.js (offline) or Google Cloud Vision
- **Book lookup** - With a.o. Open Library, Google Books, Europeana, Library of Congress
- **Book cover lookup**
- **Confidence indicators** - Shows match quality for each book
- **Export to markdown** - Compatible with Libiry and Obsidian
- **Customizable** - Change the field names to match those you use in Obsidian or Libiry
- **Works offline** - After the initial load, Tesseract.js works without internet
- **Installable** - Add to home screen on mobile devices

 The Libiry BookSpineScanner is a Progressive Web App (PWA) that identifies books with spine OCR and barcode detection. It gives you [markdown](https://en.wikipedia.org/wiki/Markdown) (text) files that can be used in Libiry, Obsidian and other tools. It works in any modern browser (Chrome, Firefox, Safari).
## How it works

### 1. Start the Libiry BookSpineScanner [here](https://sappelen.github.io/BookSpineScanner/) or with the 'Other apps' button in Libiry

### 2. Check the ![[gear.png]] Settings. Which OCR engine do you want to use? And which book databases?

### 3. Take a photo of your bookshelf (or upload a photo)

### 4. The tool detects individual book spines

### 5. The tool uses [OCR](2.2%20OCR%20engines%20used.md) to extract text from each spine

### 6. The tool looks up books in [various online databases](2.3%20Book%20databases%20used.md)

### 7. Review the results and correct mistakes

You'll see that each result has a confidence indicator:
- 🟢 **High** - correct match (>85% confidence that the OCR text matches this book in the database)
- 🟠 **Medium** - uncertain match (50-85% confidence)
- 🔴 **Low** - incorrect match (<50% confidence)

For incorrect matches (red), the preliminary book title is exported instead of the matched book title. 
Toggle the confidence indicator to change its value. 

Review each result. Expand rows to view all information.

Fix the wrong matches. 
Tip: type author and title, set the confidence indicator to green and press Lookup. The BookSpineScanner will then retain the values for author and title, but update the other fields. 

Add tags to individual books.

### 8. Export the results

Add common tags, like:
- type/analog (physical book)
- shelf/bottom-left (location)
- collection/favorites (collection)
- genre/scifi (genre)
- status/to-read (reading status)
to your books by putting them in the tag box at the bottom of the screen.

Tip: Keep your scan photos until you've verified the export. If you find errors later, you can re-scan.

Then, press Export.md or Export.zip.

### 9. Open your result files in Libiry

Move your BookSpineScanner files to a folder within your Libiry library folder. The books in the files are then shown in Libiry's book grid, alongside any digital books you might have.

## When to use

The Libiry BookSpineScanner works best when:
- You have many books to catalog
- The spine text is readable (not too small or faded)
- Your books are not too old or too damaged
- Your books are present in online databases

Some manual corrections are usually needed.

## Barcode mode

For books with a visible ISBN barcode:

- Enable "Barcode mode" in Settings
- Take a photo of the barcodes
- The app reads ISBN numbers directly from the barcodes
- Books are looked up by ISBN in various databases
- If a book is not found in these databases, a WorldCat search link is provided as the book title

## Supported platforms

| Platform | Browser         | Installation       |
| -------- | --------------- | ------------------ |
| Android  | Chrome, Firefox | Add to home screen |
| Windows  | Chrome, Edge    | Install as app     |
| macOS    | Chrome, Safari  | Install as app     |
| Linux    | Chrome, Firefox | Install as app     |
## Data and privacy

- No account required. No tracking, no analytics
- All processing happens in your browser. The only data that is sent to any server, are the book data lookups in Google Vision, Open Library etc. If you do not want that, you can choose to only use [Tesseract OCR](https://tesseractocr.org/), an open-source tool that runs entirely offline on your local machine and never uploads your data. It is compliant with strict privacy regulations like GDPR
- Your settings are stored in your browser's local storage
- Book lookup results are cached in your browser (IndexedDB) to reduce API calls

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
- In the BookSpineScanner, tap the gear icon (Settings)
- Paste your API key in the "Google Vision API Key" field
- Select "Google Cloud Vision" as OCR engine