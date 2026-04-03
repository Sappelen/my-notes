---
title: Goodreads integration
---
Import your Goodreads library into Libiry or export your Libiry catalog in Goodreads-compatible format.

## Overview

Goodreads is a popular book tracking service. Libiry's field names are compatible with Goodreads CSV exports, making it easy to:
- Import your Goodreads reading history
- Export your library for Goodreads import
- Maintain compatibility with Goodreads-based tools

## Field mapping

Some Libiry fields correspond to Goodreads fields:

| Libiry field | Goodreads CSV column |
| ------------ | -------------------- |
| booktitle    | title                |
| author       | author               |
| isbn         | ISBN                 |
| rating       | my rating            |
| publisher    | publisher            |
| pages        | number of pages      |
| year         | year published       |
| tags         | bookshelves          |
| description  | my review            |
| notes        | private notes        |

 Some Libiry fields do not exist in Goodreads:
- cover (link to cover image location or URL)
- language
- series
- series_index
- author_sort
- page_count
- publication_date
- translator
- illustrator

Some Goodreads fields do not exist in Libiry:
- Author l-f  
- Additional Authors  
- ISBN13  
- Average Rating  
- Binding  
- Original Publication Year  
- Date Read  
- Date Added  
- Bookshelves with positions  
- Exclusive Shelf  
- Spoiler  
- Read Count  
- Owned Copies

## Importing from Goodreads

### Step 1: Export from Goodreads

1. Go to [goodreads.com/review/import](https://www.goodreads.com/review/import)
2. Click "Export Library"
3. Download the CSV file

### Step 2: Convert to Markdown

Use a spreadsheet or script to convert CSV to markdown:

**Example Python script:**
```python
import csv
from pathlib import Path

def convert_goodreads_csv(csv_path, output_folder):
    with open(csv_path, 'r', encoding='utf-8') as f:
        reader = csv.DictReader(f)
        for row in reader:
            # Create markdown content
            md = f"""---
booktitle: "{row['Title']}"
author: "{row['Author']}"
isbn: "{row['ISBN']}"
rating: {int(float(row['My Rating']) * 2) if row['My Rating'] else 0}
tags: [{row['Bookshelves']}]
description: "{row['My Review']}"
notes: "{row['Private Notes']}"
---

# {row['Title']}

By {row['Author']}
"""
            # Save file
            filename = row['Title'].replace(' ', '-')[:50] + '.md'
            output_path = Path(output_folder) / filename
            output_path.write_text(md, encoding='utf-8')

convert_goodreads_csv('goodreads_export.csv', 'Books/')
```

### Step 3: Import to Libiry

Move the generated markdown files to your Libiry library folder.

## Exporting to Goodreads format

### Using Libiry2Go

1. Run Libiry2Go on your library
2. Output is in Goodreads-compatible field format
3. Create a CSV if needed for Goodreads import. You can use Obsidian Bases for this, for example

### Goodreads CSV Format

If you need to create a CSV for Goodreads:

```csv
Title,Author,ISBN,My Rating,Bookshelves,My Review,Private Notes
"The Handmaid's Tale","Margaret Atwood","9780385490818",5,"distopian, scifi","Great book!",""
"Neuromancer","William Gibson","9780441569595",5,"","",""
```

## Rating conversion

Goodreads uses 1-5 stars, Libiry uses 0-10 internally:

| Goodreads | Libiry Internal | Libiry Display |
| --------- | --------------- | -------------- |
| 1 star    | 2               | ★☆☆☆☆          |
| 2 stars   | 4               | ★★☆☆☆          |
| 3 stars   | 6               | ★★★☆☆          |
| 4 stars   | 8               | ★★★★☆          |
| 5 stars   | 10              | ★★★★★          |

**Converting:**
- Goodreads to Libiry: multiply by 2
- Libiry to Goodreads: divide by 2, round

## Bookshelves to tags

Goodreads "Bookshelves" become Libiry "tags":

**Goodreads:**
```
Bookshelves: fantasy, to-read, favorites
```

**Libiry YAML:**
```yaml
tags:
  - fantasy
  - to-read
  - favorites
```

**Libiry flat format:**
```
tags: [fantasy, to-read, favorites]
```

## Obsidian Plugins

Several Obsidian plugins sync with Goodreads:

### Booksidian

- Imports Goodreads activity automatically
- Creates book notes with YAML frontmatter
- Uses same field names as Libiry

### Book search

- Searches multiple sources including Goodreads
- Creates notes for new books
- Complements Libiry's catalog

## Maintaining sync

### One-way import (Goodreads → Libiry)

1. Export from Goodreads periodically
2. Convert new books to markdown
3. Add to Libiry library
4. Remove duplicates with Twins filter

### Manual sync

1. Read/finish in Goodreads
2. Update tags in Libiry
3. Add personal notes in Obsidian

### Automated sync

Use services like:
- IFTTT webhooks
- Goodreads API (developer account required)
- Third-party sync tools

## ISBN matching

Use ISBN for accurate matching:

1. In Goodreads, ensure ISBN is filled
2. In Libiry, ISBN enables duplicate detection
3. Book database lookups use ISBN

## Private notes

Goodreads' "Private Notes" maps to Libiry's `notes`:

```yaml
notes: "Borrowed from library, return by March"
```

These stay in your local files and are never uploaded.

## Limitations

### Goodreads API

The Goodreads API was deprecated. Current options:
- Manual CSV export/import
- Third-party tools (may be unofficial)
- RSS feeds (limited data)

### Real-time sync

No automatic sync exists. Update manually or use:
- Periodic exports
- Obsidian plugins for Goodreads
- Personal scripts

### Reading progress

Goodreads reading progress doesn't export well. Track with:
- Libiry tags: `reading`, `read`, `to-read`
- Obsidian fields: `status`, `progress`
