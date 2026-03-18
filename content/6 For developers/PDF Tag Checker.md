---
title: PDF Tag Checker
---

The PDF Tag Checker identifies PDFs that cannot read or write tags directly, and automatically creates OPF files for them.

## Purpose

Some PDFs have encryption, unusual structures, or other characteristics that prevent direct metadata editing. This utility:

1. Tests each PDF for tag read/write capability
2. Identifies problematic PDFs
3. Creates OPF buddy files for problematic PDFs
4. Reports results

## Usage

### Basic Usage

```bash
python check_pdf_tags.py [folder]
```

If no folder is specified, scans the current directory.

### Examples

```bash
# Scan C:\Books and all subfolders
python check_pdf_tags.py "C:\Books"

# Scan current folder
python check_pdf_tags.py

# Scan specific subfolder
python check_pdf_tags.py "C:\Books\Technical"
```

### Using Virtual Environment (Windows)

```batch
cd C:\Libiry
venv\Scripts\python.exe check_pdf_tags.py "C:\Books"
```

## Output

### Progress Display

```
Scanning folder: C:\Books

Found 42 PDF files. Testing tag support...

[1/42] Testing: document1.pdf... OK
[2/42] Testing: document2.pdf... FAILED: Incremental save failed
         -> Created OPF buddy file
[3/42] Testing: document3.pdf... OK
...
```

### Summary Report

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

## What Gets Tested

For each PDF, the utility:

1. **Opens** the PDF file
2. **Reads** current metadata
3. **Writes** a test tag
4. **Saves** the file (incremental save)
5. **Reads** to verify tag was saved
6. **Restores** original metadata (removes test tag)

If any step fails, the PDF is marked as problematic.

## OPF Files

### What They Are

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

### How Libiry Uses OPF files

1. When reading metadata, Libiry checks if an OPF file exists
2. If the metadata cannot be read from the PDF, they are read from the OPF instead
3. When writing metadata, the OPF is used if the data cannot be written to the PDF

## Common Failure Reasons

| Error                      | Cause                                           | Solution             |
| -------------------------- | ----------------------------------------------- | -------------------- |
| `Incremental save failed`  | PDF structure doesn't allow incremental updates | OPF file             |
| `Permission denied`        | PDF has modification restrictions               | OPF file             |
| `Tag not found after save` | PDF appears to save but doesn't persist         | OPF file             |
| `Unable to open document`  | Corrupted or unsupported PDF                    | Check file integrity |
| `PyMuPDF not installed`    | Missing dependency                              | Run install.bat      |

## When to Run

### Initial Setup

Run once on your entire library:
```bash
python check_pdf_tags.py "D:\Books"
```

### After Adding New PDFs

Run on new additions:
```bash
python check_pdf_tags.py "D:\Books\NewArrivals"
```

### After Updates

No need to re-run on already-checked PDFs. OPF files persist.

## Integration with Libiry

### Automatic Detection

When you edit tags in Libiry:

1. Libiry checks if OPF exists
2. If yes, uses OPF for tag storage
3. If no, tries direct PDF metadata
4. If that fails, creates OPF file

### Manual Pre-Check

Running `check_pdf_tags.py` in advance:
- Identifies all problematic PDFs upfront
- Creates OPF files before you need them
- Avoids errors during tag editing

## Options

Currently the script has no command-line options. It:
- Always scans recursively
- Always creates OPF files for failures
- Always shows verbose progress

## Technical Details

### Test Tag

A temporary tag `__libiry_test_tag__` is used for testing and removed after.

### Save Method

Uses PyMuPDF's incremental save with encryption preservation:
```python
doc.save(path, incremental=True, encryption=fitz.PDF_ENCRYPT_KEEP)
```

### Existing Tags

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
