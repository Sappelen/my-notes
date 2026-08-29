---
title: Libiry roadmap
---
# Future
## Version 1.0.0

### Libiry

The following functionality is planned for Libiry 1.0.0:

- Add the possibility to hide some metadata fields from the edit screen
- A mass edit functionality for all metadata fields, not just tags
- Android version
- macOS version
- Flexible length/width grid tile proportions
- Flexible distance between grid tiles

### BookSpineScanner

The following functionality is planned for the Libiry BookSpineScanner:
- Revive Tesseract functionality. The Tesseract functionality that was there originally interfered with Google Cloud Vision. So I axed it, pretty much. It is there in name only at the moment. Cutting the bookshelf photo up into strips, as was needed for Tesseract, meant worse results in Google Cloud Vision. I plan to build two separate functions now, one for Tesseract and one for Google Cloud Vision
- Add date_added and date_read

### Calibre2Libiry

No extra functionality is planned for the Calibre2Libiry app

### Libiry2Go

The following functionality is planned for Libiry2Go:
- The option to suppress the extra technical fields - exact same output as BookSpineScanner
- An option to include the entire e-book content into the markdown files
- An option to exclude timestamp metadata from the export

### Align book data

The following functionality is planned for Align book data:
- An option to only show conflicts for books that can be adjusted

# Someday or never

There are limits to the possibilities of this app.
Not all user requests will be granted. This is a simple app and that is how it was intended. 
If you have an idea for extra functionality, please contact me though. Perhaps we can make your idea come true.
And, if not, you are also totally welcome to incorporate functionality from this app into other apps. Letting me know about that is highly appreciated!

At least the following features are not on any to do list at the moment:
- A read only mode
- The possibility to save the cover separately, or to retrieve a cover url to put in the sidecar
- The possibility to select multiple tags at the same time

# Past
## Version 0.1.0

- Initial version, entirely vibecoded

## Version 0.2.0

- The vibe coded proof of concept has been refactored. This was a major refactor with 6,277 additions and 9,495 deletions. The codebase is a lot leaner now. A lot of double code has been removed, amongst other things. And the boundaries between the different modules have been minimized by moving functionality between them
- Simplification. A lot of code that was there for "backwards compatibility" has been removed. Dark mode has been removed
- The satellite apps (Align book data, Calibre2Libiry and Libiry2Go) have been rebuilt using Kivy instead of tkinter. Their UI now has the same look as the Libiry app. They now use the same folder as Libiry (the last one used there)
- The client mode of the satellite apps has been removed
- A scroll bar for tags was implemented (max n lines)

## Version 0.3.0 - 0.5.6

- Some tweaking after the first integration tests
