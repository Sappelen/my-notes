---
title: OPF files
---
##### What they are

OPF (Open Packaging Format) files are XML files that store metadata alongside an e-book. So, an OPF file is a [sidecar file](Sidecar files).

##### How Libiry uses OPF files

Libiry sees OPF as old data, inherited from Calibre.

1. When reading metadata for an e-book, Libiry checks if an OPF file exists
2. If the metadata cannot be read from the e-book itself, they are read from the OPF file instead
3. When writing metadata, Libiry stores it either in the e-book itself or in a [markdown](markdown files) [sidecar](Sidecar files), depending on your user settings. If an OPF file still exists at that point, it is cleaned up