---
title: Calibre integration
---
Calibre is a powerful e-book management tool. It rigidly enforces Author/Title/-folders, though. Libiry can work well with **any** folder structure.

It is possible to use Libiry, but also still use Calibre to maintain your book data: 
- Do not touch Calibre's folder structure
- Maintain only your EPUB and CBZ book data in Libiry
- For your CBZ books, do not maintain any tags in Libiry
- Set 'Store book data in sidecar' to No in Libiry

Note that, once you change any other book data in Libiry, it will convert Calibre's book data file into a Libiry book data file! You can start by using Libiry on copies of some your book folders, to help you decide if/how you want to use Libiry.!!!

**Workflow:**
- Use Libiry for visual browsing, searching and as a starting point to read
- Use your default e-book reader to read individual books
- Use Calibre or other tools to convert your books into other formats
- Maintain your book data either in Calibre, or in (a combination of) other tools like Libiry and Obsidian
### Calibre folder structure

Libiry allows any given folder structure. It reads:
- E-book files (EPUB, MOBI, PDF, etc.)
- Cover images
- Book data from e-book files
- Book data from Calibre sidecars
- Book data from Libiry sidecars

When a book has been edited in Libiry and 'Store book data in sidecar' is set to N,

## Book data compatibility

### What Libiry reads from Calibre books

| Calibre field                            | Libiry field     | Notes                                 |
| ---------------------------------------- | ---------------- | ------------------------------------- |
| title                                    | booktitle        | Full support                          |
| authors                                  | author           | Full support                          |
| tags                                     | tags             | Partial support                       |
| rating                                   | rating           | Calibre: 0-10, displayed as 0-5 stars |
| ISBN                                     | isbn             | Full support                          |
| publisher                                | publisher        | Full support                          |
| published                                | publication date | Full support                          |
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
- Edit in Libiry → visible in Calibre (after a refresh)

**Other formats:** May require sidecar files

### PDF tags

Calibre stores PDF tags differently:
- Calibre uses metadata.opf in the book folder
- Libiry uses the PDF keywords field or a markdown file

## Calibre plugins

### Enhanced metadata

If you use Calibre plugins for book data:
- Metadata stored in e-books propagates to Libiry
- Custom columns won't sync (these are Calibre-specific)
- Standard fields work everywhere
### Reading progress

Calibre's reading progress doesn't sync to Libiry. 
Consider using tags like reading, read, to-read.

### Cover images

When no external cover file is present, Calibre generates covers at specific sizes. Libiry extracts covers independently, so they may look slightly different. Both are correct; Libiry just re-extracts.

## Avoid conflicts

Don't edit the same book in both tools simultaneously. Make changes in one tool. Close/refresh before using the other.

## Calibre's database

Libiry never reads or modifies Calibre's metadata.db. This file can be regenerated  from Calibre's OPF files and/or the books themselves (see https://manual.calibre-ebook.com/gui.html#library), but it can also contain custom columns. These don't appear in Libiry. Therefore you are advised to consider using tags instead of custom columns for data that should be visible in Libiry.

