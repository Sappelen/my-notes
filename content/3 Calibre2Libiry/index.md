---
title: 3 Calibre2Libiry
---
With Calibre2Libiry you can convert all of Calibre's sidecar and image files from
  - metadata.opf → book.pdf.md
  - cover.jpg → book.pdf.jpg
  - cover.png → book.pdf.png
  
After that, you can change your folder structure any way you want. 

An example. If Calibre library looks like:

```
Calibre Library  
├── Margaret Atwood  
│ ├── The Handmaid's Tale (1)  
│ │ ├── The Handmaid's Tale - Margaret Atwood.epub  
│ │ ├── cover.jpg  
│ │ └── metadata.opf  
│ └── The Testaments (2)  
│ │ ├── The Testaments - Margaret Atwood.epub  
│ │ ├── cover.jpg  
│ │ └── metadata.opf 
├── William Gibson  
│ └── Neuromancer (3)  
│ │ ├── Neuromancer - William Gibson.epub  
│ │ ├── cover.jpg  
│ │ └── metadata.opf 
└── metadata.db
```

After using Calibre2Libiry, it will look like:

```
Calibre Library  
├── Margaret Atwood  
│ ├── The Handmaid's Tale (1)  
│ │ ├── The Handmaid's Tale - Margaret Atwood.epub  
│ │ ├── The Handmaid's Tale - Margaret Atwood.jpg  
│ │ └── The Handmaid's Tale - Margaret Atwood.md  
│ └── The Testaments (2)  
│ │ ├── The Testaments - Margaret Atwood.epub  
│ │ ├── The Testaments - Margaret Atwood.jpg  
│ │ └── The Testaments - Margaret Atwood.md
├── William Gibson  
│ └── Neuromancer (3)  
│ │ ├── Neuromancer - William Gibson.epub  
│ │ ├── Neuromancer - William Gibson.jpg  
│ │ └── Neuromancer - William Gibson.md 
└── metadata.db
```

You can now rearrange your books any way you want. As long as your book file and the same-named markdown and/or cover file live in the same folder, Libiry will use them. 
If you move a book in Libiry, any same-named markdown and cover file will be moved automatically as well.
You can start the tool from Libiry's main screen, with the 'Other apps' button.

# Conversion rules

For books with a metadata.opf sidecar, the book.pdf.md sidecar is filled as follows:
1. Metadata from the book itself is read
2. If a separate cover exists, it is placed in the cover field
3. If an OPF sidecar exists, its metadata (including empty values) overwrite those from the e-book. Tags from both sources are merged
4. If a markdown sidecar exists, its metadata (including empty values!) overwrite those from the e-book
5. The merged metadata is written to the markdown sidecar book.pdf.md

Just like Calibre, Libiry uses a mapping between the ISO 639-1 (2-letter) language code and the ISO 639-2 (3-letter) language code in file language_codes.txt. You can add custom mappings to the file. When the OPF file has a less precise language code (f.e. "NL") than the e-book itself (f.e. "nld"), the e-book language code is used.

If you want to make the switch from Calibre to Libiry:
1. Create a backup of your entire library
2. Optionally force regeneration of all metadata.opf sidecar files
3. Optionally extract the covers from your e-books and store them as sidecars with Calibre's Save to disk or Polish books-functionality
4. The Calibre2Libiry app will use metadata.opf as the primary source of your metadata, and the e-book metadata only as a fallback, which is the correct order
5. Use metadata.db only if you also want to transfer Calibre-specific items that are not in OPF

Note that the metadata.opf contain all the information that Calibre needs to rebuild the entire metadata.db database, using [calibredb restore_database](https://manpages.debian.org/bullseye/calibre/calibredb.1.el.html).

Note that, for books without a sidecar, the metadata inside the e-book itself is not copied into a book.pdf.md sidecar with Calibre2Libiry. If you **do** want to create sidecars for all your e-books, use [Libiry2Go](content/4%20Libiry2Go/index.md).

## Migration strategy

- Optional: If you plan to store your book data inside your books (so not in sidecar files), consider converting your books into EPUB and CBZ formats first. It will limit the number of sidecars you need
- [Export all books from Calibre](https://manual.calibre-ebook.com/generated/en/calibredb.html), including their covers and book data (in OPF files)
- Point Libiry to your Calibre library or move/copy it to your preferred location

