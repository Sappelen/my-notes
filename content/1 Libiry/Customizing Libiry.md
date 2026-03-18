---
title: Customizing Libiry
---

## Configuration files

Libiry uses a hierarchical configuration system:

1. **`customize/customize.txt`** - User overrides (highest priority)
2. **`resources/customize.txt`** - Default values
3. **Hardcoded defaults** - Fallback values

All values from customize/customize.txt can be maintained using the gear bottom in Libiry.

Likewise, you can create your own button images in folder customize. These override the button images in folder resources - as long as they have the exact same name.
## Settings location

The user settings are stored in:
- **Windows:** `C:\Users\<username>\.libiry\settings.json`
- **Linux/macOS:** `~/.libiry/settings.json`

## customize.txt format

```ini
Location: C:\Books
Background color: #6F9D9F
Button color: #793F4E
Button font color: white
Search box color: white
Tile font color: black
Background font color: black
Search box font color: black
Rounded corners y/n: Y
Only selected file types y/n: Y
Fuzzy search y/n: N
Scrollbar width: 10
Scrollbar always visible y/n: Y
Show book title y/n: Y
Show tags y/n: Y
Font size: 12

# Configurable field names
Field name cover: cover
Field name booktitle: booktitle
Field name author: author
Field name isbn: isbn
Field name rating: rating
Field name publisher: publisher
Field name year: year
Field name language: language
Field name tags: tags
Field name series: series
Field name series_index: series_index
Field name description: description
Field name notes: notes
Field name file_created: created (only used in Libiry2Go)
Field name file_modified: updated (only used in Libiry2Go)
```

## Configuration options

### Location

```ini
Location: C:\Books
```

The default folder to open when Libiry starts. Can also be set through the Settings panel.

### Colors

Hexadecimal codes ('#6F9D9F', '#FFF') and color names (white, black, red, blue) can be used. RGB tuples (111, 157, 159) cannot.

| Default setting         | Description             | Default   |
| ----------------------- | ----------------------- | --------- |
| `Background color`      | Main window background  | `#6F9D9F` |
| `Button color`          | Button background       | `#793F4E` |
| `Button font color`     | Button text             | `white`   |
| `Search box color`      | Search input background | `white`   |
| `Tile font color`       | Text on book tiles      | `black`   |
| `Background font color` | Status bar text         | `black`   |
| `Search box font color` | Search input text       | `black`   |

### Appearance

| Setting | Values | Description |
|---------|--------|-------------|
| `Rounded corners y/n` | Y/N | Enable rounded button corners |
| `Scrollbar width` | Number (pixels) | Width of scrollbar |
| `Scrollbar always visible y/n` | Y/N | Never auto-hide scrollbars |
| `Show book title y/n` | Y/N | Display title on cover tiles |
| `Show tags y/n` | Y/N | Display tags on cover tiles |
| `Font size` | Number (points) | Global font size |

### Behavior

| Setting | Values | Description |
|---------|--------|-------------|
| `Only selected file types y/n` | Y/N | Filter to configured file types |
| `Fuzzy search y/n` | Y/N | Enable fuzzy character matching |

### Field names

Customize metadata field names for compatibility with other tools:

```ini
Field name cover: cover
Field name booktitle: booktitle
Field name author: author
Field name isbn: isbn
Field name tags: tags
Field name rating: rating
Field name publisher: publisher
Field name year: year
Field name language: language
Field name series: series
Field name series_index: series_index
Field name description: description
Field name notes: notes
```

**Goodreads mapping:**
- `booktitle` → Title
- `rating` → My Rating
- `year` → Year Published
- `tags` → Bookshelves
- `description` → My Review
- `notes` → Private Notes

## selected types.txt

Located in `resources/selected types.txt` or `customize/selected types.txt`:

```
.epub
.mobi
.azw
.azw3
.pdf
.cbr
.cbz
.md
```

Only files with these extensions are displayed when "Only selected file types" is enabled.

## Cache configuration

The thumbnail cache is stored in:
- **Windows:** `C:\Users\<username>\.libiry\cache\`
- **Linux/macOS:** `~/.libiry/cache/`

The cache is automatically cleared on startup to ensure fresh covers.

## Environment variables

No environment variables are used. All configuration is file-based.

## Configuration tips

### For Obsidian Users

If you use Obsidian with specific field names:
```ini
Field name booktitle: title
Field name tags: tags
```

### For Calibre Users

Calibre uses standard field names, so defaults usually work. For custom columns:
```ini
Field name tags: #mytags
```

### For High DPI Displays

Increase font size for better readability:
```ini
Font size: 16
```

### For Touch Screens

Increase scrollbar width for easier touch:
```ini
Scrollbar width: 20
Scrollbar always visible y/n: Y
```
