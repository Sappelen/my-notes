# Main window

![[https://marjonw.wordpress.com/wp-content/uploads/2026/03/libiry-grid.png]]

```
┌────────────────────────────────────────────────────────────────────────┐
│ ← 🔄                      Search... 🔍                   ℹ️ ⚙️ 𖣯 👥  |
|                           C:\Books\Fantasy            [Choose Folder]  │
├────────────────────────────────────────────────────────────────────────┤
│                                                                        │
│  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐            │
│  │        │  │        │  │        │  │        │  │        │            │
│  │        │  │ Cover  │  │ Cover  │  │ Cover  │  │ Cover  │            │
│  │ Folder │  │  Here  │  │  Here  │  │  Here  │  │  Here  │            │
│  │        │  │        │  │        │  │        │  │        │            │
│  │        |  │ Title  │  │ Title  │  │ Title  │  │ Title  │            │
│  └────────┘  └────────┘  └────────┘  └────────┘  └────────┘            │
│                                                                        │
│  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐                        │
│  │        │  │        │  │        │  │        │                        │
│  │ Cover  │  │ Author │  │ Cover  │  │ Cover  │                  ║     │
│  │  Here  │  │ Title  │  │  Here  │  │  Here  │                  ║     │
│  │        │  │  Only  │  │        │  │        │                  ▼     │
│  │ Title  │  │        │  │ Title▲ │  │ Title🔺│                        │
│  └────────┘  └────────┘  └────────┘  └────────┘                        │
│                                                                        │
│  All books, No tag, #tag1, #tag2              [Edit] [Move] [Delete]   │
│  1 folder, 8 files (3 selected)                                        │
└────────────────────────────────────────────────────────────────────────┘
```

## Top

### Action buttons

| Button | Icon | Function |
|--------|------|----------|
| Up | ←  | Move up one folder level |
| Refresh | 🔄 | Reload current view |
| Settings | ⚙️ | Open settings panel |
| About | ℹ️ | Show application info |
| Other apps | 𖣯 | Shows the other Libiry apps |
| Twins | 👥 | Toggle duplicate detection |

### Search box

Type to search within current folder and all subfolders (up to 10 levels).

### Location bar

Shows the current folder path. Click on the folder button at the right to navigate to another folder.

## Grid area

### Folder tiles
- Display folder icon and name
- Click to navigate into folder
- Can contain subfolders and books

### Book tiles
- Display cover image when available
- Show author + title overlay when no cover
- Optional title overlay on covers

### Visual indicators

| Indicator | Meaning |
|-----------|---------|
| 🔺 Red triangle | Book has "summary" tag |
| △ Gray triangle | Book has "analog" tag |

### Selection

- **Click** - Select single book
- **Ctrl+Click** - Add to selection
- **Ctrl+A** - Select all visible books
- **Right-click** - Context menu

## Bottom

### Tag list

- **All books** - Show all books (click to reset filter)
- **No tag** - Filter to books without tags
- **Tags** sorted by frequency
- **...** indicator that more than 99 tags are available for this selection

### Status bar

- **Selected count** - Number of selected books
- **Total count** - Total books in current view
- **Book information** when a single book is selected
- **Action information** about the last requested action

### Action buttons

| Button | Function                              |
| ------ | ------------------------------------- |
| Edit   | Edit metadata                         |
| Move   | Move selected files to another folder |
| Delete | Move selected files to trash          |

## Settings panel

### Location
- Set default library folder
- Persists between sessions

### Colors
Customize all colors:
- Background
- Buttons
- Text
- Search box
- Tiles

### Options

| Setting | Description |
|---------|-------------|
| Rounded corners | Enable/disable rounded buttons |
| Only selected file types | Filter by configured file types |
| Fuzzy search | Enable character-sequence matching |
| Scrollbar width | Adjust scrollbar size |
| Scrollbar always visible | Never auto-hide scrollbars |
| Show book title | Display title on cover tiles |
| Show tags | Display tags on cover tiles |
| Font size | Adjust all text sizes |

### Field names
Remap metadata field names for compatibility with:
- Goodreads exports
- Obsidian plugins
- Calibre libraries
- Custom setups

## Scrolling

### Scrollbar
- Always visible (configurable)
- Clickable to jump to position
- Draggable for smooth scrolling
- Width adjustable in settings

### Mouse/touch
- Mouse wheel to scroll
- Touch/drag to scroll on touch devices
- Click scrollbar track to jump

## Accessibility notes

Libiry uses Kivy, which creates its own UI rather than using native OS controls. This means:
- Screen readers are not fully supported
- Keyboard navigation is limited
- High contrast themes must be configured manually

For users requiring screen reader support, consider using Calibre or other native applications alongside Libiry.
