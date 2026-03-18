---
title: Libiry features
---

## Visual book grid

Libiry displays your books as a grid of cover images, making it easy to browse your collection visually.

### Cover display
- Covers are automatically extracted from EPUB, PDF, MOBI, CBZ files
- An SQLite-based cache means fast loading
- When no cover is available, author + title are displayed

### Visual indicators
- Red triangle - Book has "summary" tag
- Gray triangle - Book has "analog" tag (physical book)
- Folder icons - Navigable folder tiles

## Search and navigation

### Search
- Searches up to 10 levels deep
- Case-insensitive
- Fuzzy search is possible (matches characters in any order)
- Type one of the supported file types in the search box (f.e. ".epub") to search on that file type

### Navigation
- Click Up to go to the parent folder
- Click Refresh to reload the current view

## Tag Management

### Viewing tags
- Tags displayed in status bar
- Sorted by frequency (most common first)
- Click any tag to filter

### Tag filtering
- "All books" or "...": Show everything
- "No tag": Show books without any tags
- Click a tag to show only books with that tag

### Editing tags
1. Select one or more books
2. Right-click or use context menu
3. Click "Edit Tags"
4. Add new tags or remove existing ones

Tags are stored:
- **EPUB** - In the ebook file itself
- **MOBI/AZW/AZW3** - In OPF sidecar file
- **CBR** - In OPF sidecar file
- **CBZ** - In ComicInfo.xml
- **PDF** - In file metadata or OPF sidecar
- **Markdown** - In the file content

## Duplicate detection (Twins filter)

Find duplicate books in your collection:

1. Click the Twins button
2. Libiry scans all subfolders recursively
3. Duplicates are detected by:
   - Exact ISBN match
   - Normalized title + author match

### Normalization Rules
- Removes articles: "The", "A", "An", "De", "Het", "Een"
- Removes author suffixes: "Jr", "Sr", "PhD"
- Sorts author name parts alphabetically
- Case-insensitive comparison

## File Management

### Move Files
1. Select files
2. Right-click → Move
3. Choose destination folder

### Delete Files
1. Select files
2. Right-click → Delete
3. Confirm deletion

Files are moved to the system trash (recoverable) if the system settings allow that. Otherwise, they are permanently deleted.

### Warnings
- Moving/deleting multi-book markdown files shows a warning
- Nested folders show a warning before deletion

## Customization

### Colors
All colors are customizable:
- Background color
- Button color
- Button font color
- Search box color
- Tile font color
- Background font color
- Search box font color

### Appearance
- Straight or rounded corners
- Scrollbar width
- Font size
- Hide or show book title
- Hide or show tags

### File Types
Configure which file types to display in `selected types.txt`

## Metadata Extraction

### Supported Formats

| Format   | Cover | Title | Author | Tags | Other          |
| -------- | ----- | ----- | ------ | ---- | -------------- |
| EPUB     | ✓     | ✓     | ✓      | ✓    | Full metadata  |
| MOBI/AZW | ✓     | ✓     | ✓      | ✓*   | Basic metadata |
| PDF      | ✓     | ✓     | ✓      | ✓    | Full metadata  |
| CBZ      | ✓     | ✓     | ✓      | ✓    | ComicInfo.xml  |
| CBR      | ✓     | ✓     | ✓      | ✓*   | Basic          |
| Markdown | ✓     | ✓     | ✓      | ✓    | All fields     |
Uses OPF sidecar files

### Markdown Support
Two formats are supported:

**YAML Frontmatter (compatible with Obsidian):**
```yaml
---
cover: "cover.jpg"
booktitle: "The Book Title"
author: "Author Name"
tags: [fiction, fantasy]
---
```

**Flat Format (Libiry/BookSpineScanner):**
```
[cover]: cover.jpg
[booktitle]: The Book Title
[author]: Author Name
[tags]: fiction, fantasy
```

## Goodreads Compatibility

Field names follow Goodreads CSV format:
- `booktitle` → Title
- `author` → Author
- `rating` → My Rating
- `tags` → Bookshelves
- `description` → My Review
- `notes` → Private Notes

All field names are configurable for compatibility with existing setups.

## Performance Features

- **Lazy loading** - Only visible items are loaded
- **SQLite cache** - Thumbnails are cached for instant loading
- **Background scanning** - UI stays responsive during scans
- **Limited recursion** - Max 100 books per markdown file
