---
title: Welcome to Libiry
---

![[https://marjonw.wordpress.com/wp-content/uploads/2026/03/libiry-grid-1.png]]

Welcome to the official Libiry site. Libiry is a set of tools that helps you to manage your entire book collection: physical books on shelves, ebooks, audiobooks, book notes and summaries. 
The set consists of four tools that work together.

| Component                                                            | Description                                                                  | Platform                            |
| -------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ----------------------------------- |
| [**Libiry**](1%20Libiry/index.md)                                    | Browse and maintain your physical and digital library                        | Windows, Linux, macOS, Android, iOS |
| [**LibiryBookSpineScanner**](2%20Libiry%20Bookspinescanner/index.md) | Scan or upload bookshelf photos and extract book metadata to markdown files  | Web - Any device                    |
| [**Calibre2Libiry**](index.md)                                       | Rename your Calibre OPF and cover files for use in your own folder structure | Windows, Linux, macOS, Android, iOS |
| [**Libiry2Go**](4%20Libiry2Go/index.md)                              | Create portable markdown files with metadata of your book collection         | Windows, Linux, macOS               |
|                                                                      |                                                                              |                                     |

Libiry works with your own book folder structure. 
It visualizes ALL of your books and zines, with or without an ISBN number.
There's no separate database.
You can choose your own markdown field names. 

With the Libiry BookspineScanner, you can add your physical books to your ebook collection with only one photo per book shelf. Taking stock of your analog books is not a big project anymore. It can easily be done in parts, too.
## Quick links

### Getting started
- [Quick start guide](Getting%20started%20with%20Libiry.md) - Get up and running in minutes
- [Installation guide](Libiry%20installation%20guide.md) - Detailed installation instructions
- [Your first scan](Scanning.md) - Start cataloging your physical books

### Features
- [Libiry Features Overview](Libiry%20features.md)
- [Supported file formats!!!](Supported%20file%20formats!!!.md)
- [Metadata & Tags](Metadata%20handling!!!.md)
- [Keyboard Shortcuts](Keyboard%20shortcuts.md)

### [[5 Integration with other tools/index|Integration with other tools]]

### [[6 For developers/index|Information for developers]]

## Metadata per format

| Format        | Read | Write metadata | Notes                                                                                                                                                                           |
| ------------- | ---- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| EPUB          | ✓    | ✓              | Full metadata support                                                                                                                                                           |
| MOBI/AZW/AZW3 | ✓    | ✓              | OPF files used for metadata storage                                                                                                                                             |
| PDF           | ✓    | ✓              | Title, author, description and tags can be maintained in most PDFs. Sidecars are needed for some PDFs and also for isbn, year, language, series, rating, notes, publisher, etc. |
| CBZ           | ✓    | ✓              | Metadata are supported for most fields, OPF files are only needed for isbn, author_sort and publication_date                                                                    |
| CBR           | ✓    | ✓              | OPF files used for metadata storage                                                                                                                                             |
| Markdown      | ✓    | ✓              | Full metadata support                                                                                                                                                           |
| Other formats | ✓    | ✓              | OPF files used for metadata storage                                                                                                                                             |

## Community and support

- [[Contributing]]
- [GitHub repository](https://github.com/sappelen/Libiry)
- [Report issues](https://github.com/sappelen/Libiry/issues)

---

*Libiry is open-source software released under the [Creative Commons 1.0 License]([https://github.com/Sappelen/BookSpineScanner#CC0-1.0-1-ov-file](https://wiki.creativecommons.org/wiki/CC0_1.0_Universal)).*
