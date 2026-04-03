  When metadata_in_sidecar is True:
  - EPUB → saves to sidecar instead of internal OPF
  - PDF → saves to sidecar instead of PDF metadata fields
  - CBZ → saves to sidecar instead of ComicInfo.xml

| Field            | EPUB                          | PDF                             | CBZ                         | Other    |    
| ---------------- | ----------------------------- | ------------------------------- | --------------------------- |  ----------- | 
| booktitle        | OPF (dc:title)                | Native + OPF                    | ComicInfo.xml               | Markdown    |   
| author           | OPF (dc:creator)              |  Native + OPF                    | ComicInfo.xml               | Markdown           |
| author_sort      | OPF (opf:file-as)             |  OPF                             | OPF                         | Markdown         |
| isbn             | OPF (dc:identifier)           |  OPF                             | OPF                         | Markdown            |
| cover            | Cover image in EPUB           |  -                               | 1st                         | URL in Markdown     |
| rating           | calibre:rating meta           | OPF                             | ComicInfo.xml               | Markdown        |
| publisher        | OPF (dc:publisher)            | OPF                             | ComicInfo.xml               |  Markdown     |
| year             | OPF (dc:date)                 |  OPF                             | ComicInfo.xml               |  Markdown      |
| publication_date | OPF (dc:date)                 |  OPF                             | OPF sidecar                 |  Markdown        |
| language         | OPF (dc:language)             |OPF                             | ComicInfo.xml (LanguageISO) |  Markdown         |
| pages            | calibre:pages meta            | OPF                             | ComicInfo.xml  (PageCount)  |  Markdown        |
| tags             | OPF (dc:subject)              |  Native (subject/keywords) + OPF | (Tags)                      |  Markdown        |
| series           | calibre:series meta           | OPF                             | ComicInfo.xml (Series)      |  Markdown         |
| series_index     | calibre:series_index          |  OPF                             | ComicInfo.xml  (Number)     |  Markdown         |
| translator       | OPF (dc:contributor role=trl) |  OPF                             | ComicInfo.xml               |  Markdown        |
| illustrator      | OPF (dc:contributor role=ill) |  OPF                             | ComicInfo.xml(Penciller)    |  Markdown         |
| description      | OPF (dc:description)          | Native (subject) +  OPF         | ComicInfo.xml(Summary)      | Markdown        |
| notes            | calibre:user_notes            | OPF                             | ComicInfo.xml  (Notes)      | Markdown         |

# Legenda

  - Native: Directly from the file format itself
  - OPF: Open Packaging Format XML (within EPUB or as sidecar file)
  - OPF sidecar: External .opf file next to the book (f.e. book.mobi.opf)
  - ComicInfo.xml: Standard comic metadata format (within CBZ)
  - YAML frontmatter: Markdown metadata in between --- markers

# Remarks

  1. MOBI/AZW/AZW3: Alle metadata comes from an OPF sidecar because the ebook meta library is unreliable
  2. CBR: RAR-formaat is protected, so everything via OPF sidecar
  3. PDF: Native metadata (title, author, keywords) + OPF sidecar for fields the PDF doesn't support
  4. Rating: Calibre uses 0-10, Libiry shows 0-5 (automatic conversion)
  