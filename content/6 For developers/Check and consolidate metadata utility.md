---
title: Check and consolidate metadata utility
---
This tool:
- Removes redundant sidecars (those where all fields are empty)
- Checks if there are any conflicting metadata (sidecar metadata differ from file metadata)
- Tests PDFs and creates sidecar files for problematic ones
- ==Incorporates metadata into PDFs for those PDFs where metadata can be written directly into the PDF==
- Generates a full report

## Use cases


When you have cleaned up some of your metadata outside of Libiry (for example in Obsidian), your sidecars may have become empty shells. With this tool you can delete empty sidecars completely.

Some PDFs have encryption, unusual structures or other characteristics that prevent direct metadata editing. This tool identifies PDFs that cannot read or write metadata directly, and automatically creates OPF files for them.


## Usage

  There are 3 executables with which you can start this function:
  - check_and_consolidate_metadata.bat - Windows (double click)
  - check_and_consolidate_metadata.sh - Linux/macOS (bash)
  - check_and_consolidate_metadata.ps1 - PowerShell (cross platform)

### Basic usage

```bash
python check_pdf_tags.py [folder]
```

If no folder is specified, the function scans the current directory.

### Examples

```bash
# Scan C:\Books and all subfolders
python check_pdf_tags.py "C:\Books"

# Scan current folder
python check_pdf_tags.py

# Scan specific subfolder
python check_pdf_tags.py "C:\Books\Technical"
```

### Using virtual environment (Windows)

```batch
cd C:\Libiry
venv\Scripts\python.exe check_pdf_tags.py "C:\Books"
```

## Output

### Progress display

```
Scanning folder: C:\Books

Found 42 PDF files. Testing tag support...

[1/42] Testing: document1.pdf... OK
[2/42] Testing: document2.pdf... FAILED: Incremental save failed
         -> Created OPF buddy file
[3/42] Testing: document3.pdf... OK
...
```

### Summary report

```
============================================================
Results:
  Total PDFs:     42
  Tag support OK: 38
  Tag support FAILED: 4

Problematic PDFs:
  - C:\Books\old_scan.pdf: Incremental save failed
  - C:\Books\encrypted.pdf: Permission denied
  - C:\Books\complex.pdf: Tag not found after save
  - C:\Books\corrupted.pdf: Unable to open document

OPF buddy files created for 4 PDFs.
Tags for these PDFs will be stored in the OPF files.
```

## What gets tested

### Metadata inconsistent?

For language codes, Libiry uses a mapping between ISO 639-1 (2-letter) and ISO 639-2 (3-letter) in file language_codes.txt. You can add custom mappings to the file. When your epub has language code nld, and your sidecar file has NL, that is not seen as inconsistent.

When the OPF has a less precise language code (like "NL") and the EPUB itself has the more precise code (like "nld"), copying "NL" to the sidecar adds no value. Let me implement this logic in Calibre2Libiry.

For each PDF, the utility:

1. **Opens** the PDF file
2. **Reads** the current metadata
3. **Writes** a test tag
4. **Saves** the file (incremental save)
5. **Reads** to verify the tag was saved
6. **Restores** the original metadata (and thus removes the test tag again)

If any step fails, the PDF is marked as problematic.

## OPF files

### What they are

OPF (Open Packaging Format) files are XML files that store metadata alongside the PDF. When Libiry encounters a problematic PDF, it uses the OPF file instead of the PDF's internal metadata.

### Structure

For a file named f.e. `book.pdf`, an accompanying OPF file `book.pdf.opf` is created:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<package xmlns="http://www.idpf.org/2007/opf" version="3.0">
  <metadata xmlns:dc="http://purl.org/dc/elements/1.1/">
    <dc:subject>fiction</dc:subject>
    <dc:subject>fantasy</dc:subject>
  </metadata>
</package>
```

### How Libiry uses OPF files

1. When reading metadata, Libiry checks if an OPF file exists
2. If the metadata cannot be read from the PDF, they are read from the OPF instead
3. When writing metadata, the OPF is used if the data cannot be written to the PDF

## Common failure reasons

| Error                      | Cause                                           | Solution             |
| -------------------------- | ----------------------------------------------- | -------------------- |
| `Incremental save failed`  | PDF structure doesn't allow incremental updates | OPF file             |
| `Permission denied`        | PDF has modification restrictions               | OPF file             |
| `Tag not found after save` | PDF appears to save but doesn't persist         | OPF file             |
| `Unable to open document`  | Corrupted or unsupported PDF                    | Check file integrity |
| `PyMuPDF not installed`    | Missing dependency                              | Run install.bat      |

## When to run

### Initial setup

Run once on your entire library:
```bash
python check_pdf_tags.py "D:\Books"
```

### After adding new PDFs

Run on new additions:
```bash
python check_pdf_tags.py "D:\Books\NewArrivals"
```

### After updates

No need to re-run on already-checked PDFs. OPF files persist.

## Integration with Libiry

### Automatic detection

When you edit tags in Libiry:

1. Libiry checks if an OPF file exists
2. If so, it uses the OPF file for metadata storage
3. If not, it tries to edit PDF metadata directly
4. If that fails, it creates an OPF file

### Manual pre-check

Running `check_pdf_tags.py` in advance:
- Identifies all problematic PDFs upfront
- Creates OPF files before you need them
- Avoids errors during tag editing

## Options

Currently the script has no command-line options. It:
- Always scans recursively
- Always creates OPF files for failures
- Always shows verbose progress

## Technical details

### Test tag

A temporary tag `__libiry_test_tag__` is used for testing and removed after.

### Save method

Uses PyMuPDF's incremental save with encryption preservation:
```python
doc.save(path, incremental=True, encryption=fitz.PDF_ENCRYPT_KEEP)
```

### Existing tags

If the PDF already has tags (keywords), they are:
1. Read before testing
2. Preserved during test
3. Copied to OPF file on failure

## Troubleshooting

### "PyMuPDF not installed"

Install the dependency:
```bash
pip install PyMuPDF
```

Or re-run `install.bat`.

### Script hangs on a file

Some corrupted PDFs may cause hangs. Press Ctrl+C to skip and continue.

### OPF files not created

Check:
- Write permissions in the folder
- Disk space available
- File isn't locked by another program
