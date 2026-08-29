---
title: 5 Align book data
---
This tool:
- Checks if there are any conflicting book data (where the sidecar metadata differ from the book metadata)
- Cleans up redundant [sidecars](Sidecar files)
- Generates a full report

You can start the tool from Libiry's main screen, with the 'Other apps' button.
You do not need this tool to use Libiry. It is optional. 
## Use cases

- When you start using Libiry, you can run this utility to check the quality of your book data 
- When you have changed some of your metadata outside of Libiry (for example in Obsidian), you may want to check the quality of your book data again
- When you have sidecars in your library, but want to start saving your book data directly into your books, change the 'Store metadata in sidecar' setting from Y to N. Then, clean up any redundant sidecars with this tool

## Output


```
======================================================================
LIBIRY BOOK METADATA ALIGNMENT REPORT
Date: 2026-08-05 10:17:47
Folder: /home/Books
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