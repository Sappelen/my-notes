---
title: 5 Align book data
---
This tool:
- Checks if there are any conflicting book data (t.i. the book data in the [sidecar](Sidecar files) differ from the book data in the book itself)
- Cleans up redundant sidecars
- Generates a full report
- Can be executed in preview mode to check the quality of your book data

You can start the tool from Libiry's main screen, with the 'Libiry apps' button.
You do not need this tool to use Libiry, it is entirely optional. 

## Use cases

- When you start using Libiry and want to review the quality of your book data 
- When you have changed some of your book data outside of Libiry (for example in Obsidian), and suspect that books and book sidecars may have become inconsistent with each other
- Just after you changed the 'Store book data in sidecar' setting from N to Y (or vice versa), if you want all (or none) of your books to have sidecars immediately
## Output


```
======================================================================
LIBIRY BOOK METADATA ALIGNMENT REPORT
Date: 2026-08-05 10:17:47
Folder: C:\Books
======================================================================

----------------------------------------------------------------------
1. REDUNDANT SIDECARS
----------------------------------------------------------------------
Sidecars found: 34
Redundant sidecars removed: 0

----------------------------------------------------------------------
2. METADATA CONFLICTS
----------------------------------------------------------------------
Files with conflicts: 1

File: Romans Engels/Jack Kerouac/On the road/On The Road - Jack Kerouac.epub
tags:
Native:  Literature: Classics
Sidecar: read, Literature: Classics

======================================================================
SUMMARY
======================================================================
Redundant sidecars removed: 0
Metadata conflicts found: 1

ACTION REQUIRED: Review the metadata conflicts and decide which
value is correct (native or sidecar).
```

## What to do when conflicts are found?

If the native book data are correct, adjust the sidecar.
If the sidecar is correct, adjust the book itself.
Then run the tool again.