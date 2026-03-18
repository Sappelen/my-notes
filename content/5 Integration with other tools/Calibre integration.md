---
title: Calibre integration
---

Calibre is a powerful ebook management tool. It rigidly enforces `Author/Title/` folders, though. Libiry can work with that folder structure as well, but does not enforce it.

Because Libiry allows you to store your books any way you want, the 

When you maintain book metadata, you must either do that in Calibre or in Libiry. Because Libiry allows you to have your own folder structure, Calibre's OPF solution will not work.  or your metadata however, but has a different way of editing metadata when you want to edit tags and other book metadata, complements Calibre by providing:
- Visual grid-based browsing
- Quick tag filtering and editing
- Physical book cataloging
- Mobile-friendly interface

**Typical workflow:**
- Use Libiry for visual browsing, searching, metadata management, and as a starting point to read
- Use Calibre to read individual books, track your progress in these books and convert them to other formats

## Setup

### Optional: convert some book formats to streamline your book collection first

Libraries can get messy when they contain lots of small files. If you like to use your own folder structure but would like to limit the number of OPF files, consider converting your CBR files to CBZ files and your MOBI, AZW and AZW3 files to EPUB files. You can do that in Calibre. It will eliminate the need for separate OPF files for these books.
You can 

### Point Libiry to your Calibre Library

1. Open Libiry Settings
2. Set the Location to your Calibre library folder
   - Default Windows: `C:\Users\<user>\Calibre Library`
   - Default macOS: `~/Calibre Library`
   - Default Linux: `~/Calibre Library`
3. Save settings

### Calibre library structure

Calibre organizes books by author:
```
Calibre Library  
├── Margaret Atwood  
│ ├── The Handmaid's Tale (1)  
│ │ ├── The Handmaid's Tale - Margaret Atwood.epub  
│ │ ├── cover.jpg  
│ │ └── metadata.opf  
│ └── The Testaments (2)  
│ └── ...
├── William Gibson  
│ └── Neuromancer (3)  
│ └── ...
└── metadata.db
```

Libiry allows any given folder structure. It reads all folder reads:
- Ebook files (EPUB, MOBI, PDF, etc.)
- Cover images (cover.jpg)
- Metadata from ebook files

With the tool [Calibre2Libiry](3%20Calibre2Libiry/index.md) you can rename all of Calibre's opf files and image files from
  - metadata.opf → book.pdf.opf
  - cover.jpg → book.pdf.jpg
  - cover.png → book.pdf.png
  
  After that, you can change your folder structure any way you want. 

## Metadata compatibility

### What Libiry reads from Calibre books

| Calibre field                            | Libiry field     | Notes                                 |
| ---------------------------------------- | ---------------- | ------------------------------------- |
| title                                    | booktitle        | Full support                          |
| authors                                  | author           | Full support                          |
| tags                                     | tags             | Partial support                       |
| rating                                   | rating           | Calibre: 0-10, displayed as 0-5 stars |
| ISBN                                     | isbn             | Full support                          |
| publisher                                | publisher        | Full support                          |
| published                                | year             | Year extracted                        |
| comments                                 | description      | Full support                          |
| series                                   | series           | Full support                          |
| series index                             | series_index     | Full support                          |
| opf:file-as attribute op dc:creator      | author_sort      | Full support                          |
| dc:contributor with opf:role="trl"       | translator       | Full support                          |
| dc:contributor with opf:role="ill"       | illustrator      | Full support                          |
| complete dc:date (YYYY-MM-DD)            | publication_date | Full support                          |
| Calibre metadata or rendition:page-count | pages            | Full support                          |
| language                                 | language         | Full support                          |
 
### Tag synchronization

**EPUB files:** Tags sync both ways
- Edit in Calibre → visible in Libiry
- Edit in Libiry → visible in Calibre (after refresh)

**Other formats:** May require OPF files

### PDF tags

Calibre stores PDF tags differently:
- Calibre uses metadata.opf in the book folder
- Libiry uses the PDF _keywords_ field or an OPF file

For best compatibility, use Libiry's OPF files for PDFs.

## Calibre plugins

### Enhanced metadata

If you use Calibre plugins for metadata:
- Metadata stored in ebooks propagates to Libiry
- Custom columns don't sync (Calibre-specific)
- Standard fields work everywhere

### Reading progress

Calibre's reading progress doesn't sync to Libiry. 
Consider using tags like _reading_, _read_, _to-read_.

### Calibre custom columns

Calibre custom columns (_#column_) are stored in _metadata.db_, not in ebook files. These don't appear in Libiry. 
Consider using tags instead of custom columns for data that should be visible in Libiry.

### Cover images

Calibre generates covers at specific sizes. Libiry extracts covers independently, so covers may look slightly different. Both are correct; Libiry just re-extracts.

### OPF metadata files

Calibre creates _metadata.opf_ files in book folders. These are Calibre-specific and different from Libiry's OPF metadata files.

## Avoiding conflicts

### File locking

Don't edit the same book in both tools simultaneously. Make changes in one tool. Close/refresh before using the other.

### Database integrity

Libiry never modifies Calibre's _metadata.db_. 