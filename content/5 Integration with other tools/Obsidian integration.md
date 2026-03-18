---
title: Obsidian integration
---
Obsidian is a powerful app that uses markdown files. Libiry's markdown support makes it fully compatible with Obsidian vaults. Use Libiry alongside Obsidian for comprehensive book management and knowledge linking. It can handle extra fields anddifferent field sequences.

**Use cases:**
- Create book notes linked to your library
- Track reading progress with Dataview
- Build a personal knowledge base around your books
- Sync book metadata across devices

## Setup

### Option 1: Libiry2Go export

1. Run [Libiry2Go](4%20Libiry2Go/index.md) on your book library
2. Use the "one file per book" mode
3. Place the output in your Obsidian vault

```bash
python libiry2go.py "C:\Books" "C:\Obsidian\Books" 1
```

### Option 2: Libiry BookSpineScanner export

1. Scan your physical books
2. Use the "one file per book" mode
3. Place the output in your Obsidian vault
### Option 3: Direct library access

1. Place your library folder in your Obsidian vault
2. Or point Obsidian to your library folder
3. Books and book notes coexist
## File Format

Libiry uses YAML frontmatter compatible with Obsidian:

```yaml
---
cover: https://covers.openlibrary.org/b/isbn/9780385490818-L.jpg
booktitle: "The Handmaid's Tale"
author: "Margaret Atwood "
isbn: "9780385490818 "
tags:
  - distopian
  - scifi
  - read  
rating: 5
---

# The Handmaid's Tale 

My notes about this book...
```
## Field name configuration

You can adjust the field names Libiry and Libiry BookSpineScanner use in the tool's settings screen. Match the field names to the ones you use in Obsidian.

```ini
Field name booktitle: title
Field name description: summary
```

**Result:**
```yaml
---
title: "The Handmaid's Tale"
summary: "Offred is a Handmaid in the Republic of Gilead..."
---
```

# Note

In Libiry and other book management tools, you can use almost anything as a tag (for example: "Columns & Interviews Language: English"). In Obsidian these kind of tags will be considered incorrect.
## Obsidian Plugins

### Dataview

Query your books with Dataview:

```dataview
TABLE author, rating, tags
FROM "Books"
WHERE rating >= 8
SORT rating DESC
```

**Reading list:**

```dataview
LIST
FROM "Books"
WHERE tags = "reading"
SORT file.file_modified DESC
```

### Book search

The Book Search plugin can create book notes:
- Searches by ISBN, title, or author
- Creates markdown with YAML frontmatter
- Compatible with Libiry field names

### Booksidian

The Booksidian plugin for Goodreads sync:
- Imports Goodreads reading activity
- Creates book notes automatically
- Uses the same field format as Libiry

## Linking books

### Internal links

Reference books in your notes:
```markdown
I loved [[The Handmaid's Tale]] - see my full review.

[[Neuromancer]] reminded me of ...
```

### Tags

Use Obsidian tags for organization:
```yaml
tags:
  - fiction
  - fantasy
  - read2026
```

Nested tags work too:
```yaml
tags:
  - books/fantasy
  - status/read
```

## Cover images

Covers

URL covers and local cover images can both be displayed in Obsidian:
```yaml
cover: "https://covers.openlibrary.org/b/isbn/9780547928227-L.jpg"
```

View with: `![cover]({{cover}})`

```yaml
cover: "![[covers/handmaid.jpg]]"
```

```yaml
cover: "covers/handmaid.jpg"
```

## Syncing changes

### From Libiry to Obsidian

1. Edit tags in Libiry
2. Re-run the Libiry2Go export
3. Your book files will be overwritten

### Quickadd in Obsidian

Use Quickadd to create book notes:
1. Install the Quickadd plugin
2. Create a macro with Book search
3. Apply your book template
4. Fill in the metadata automatically

## Obsidian's Book search plugin

Libiry2Go files are compatible with Obsidian's Book search plugin:
- Frontmatter fields match the expected format
- Cover URLs work with image embedding
- Tags appear in Obsidian's tag system
### From Obsidian to Libiry

1. Edit the YAML frontmatter in Obsidian
2. Press the refresh button in Libiry
