---
title: 3. Calibre2Libiry
---
If you want to move from Calibre to Libiry, you can use this tool to convert all of Calibre's metadata files to Libbiry metadata files:
  - metadata.opf is converted to book.pdf.md, but not deleted
  - cover.jpg is renamed to book.pdf.jpg
  - cover.png is renamed to book.pdf.png
  
After that, you are no longer bound to Calibre's folder structure.
As long as your book file and the same-named markdown and/or cover file live in the same folder, Libiry will use them. 
If you move a book in Libiry, the markdown and cover files will be moved as well.

Just like Calibre, Libiry uses a mapping between the ISO 639-1 (2-letter) language code and the ISO 639-2 (3-letter) language code in file language_codes.txt. You can add custom mappings to the file. When the OPF file has a less precise language code (like "NL") and the EPUB itself has the more precise code (like "nld"), the language code is not copied into the markdown sidecar.
