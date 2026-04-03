
Common issues and solutions for Libiry.

## Installation Issues

### "Python not found"

**Problem:** Running `install.bat` or `run.bat` shows Python not found.

**Solution:**
1. Install Python 3.12 from [python.org](https://www.python.org/downloads/)
2. During installation, check "Add Python to PATH"
3. Restart your terminal/command prompt
4. Run `python --version` to verify

### "Kivy installation fails"

**Problem:** pip fails to install Kivy.

**Solution:**
```bash
# Try installing with base dependencies only
pip install kivy[base]

# Or install pre-built wheel
pip install kivy --pre --extra-index-url https://kivy.org/downloads/simple/
```

### "PyMuPDF installation fails"

**Problem:** PyMuPDF (fitz) fails to compile.

**Solution:**
```bash
# Windows - install Visual Studio Build Tools first
# Linux
sudo apt install libmupdf-dev mupdf-tools

# macOS
brew install mupdf
```

## Application Issues

### Application won't start

**Problem:** Double-clicking `run.bat` does nothing.

**Solution:**
1. Check if there any Python processes still running on your computer. Close these or restart your computer
2. Run `run_debug.bat` instead to see error messages
3. Check if virtual environment exists in `venv/` folder
4. Re-run `install.bat`

### Blank window / no books shown

**Problem:** Libiry opens but shows nothing.

**Solutions:**
1. Check Settings → Location is set correctly
2. Verify the folder contains supported file types
3. Check the "Only selected file types" setting
4. Press F5 to refresh

### Slow startup

**Problem:** Libiry takes a long time to start.

**Solutions:**
1. Large libraries take longer on the first scan
2. Check your network connection (cover lookup may timeout for slow connections)
3. Move your library to SSD if on HDD
4. Reduce your folder depth (fewer nested folders)
5. Uncheck the 'Show tags' box in Settings

## Display issues

### Covers not showing

**Problem:** Books display without covers.

**Solutions:**
1. Check internet connection (for online lookup)
2. Verify ebooks contain embedded covers
3. Clear cache: delete `~/.libiry/cache/`
4. For markdown files, check cover field path is valid

### Only one cover shown for a multibook file

**Problem:** A markdown file contains multiple books, but only one cover is shown in the grid.

**Solution:** Change your Libiry field names to match those in the markdown file.

### Text too small/large

**Problem:** UI elements are wrong size.

**Solution:**
Change your font size.

### High DPI scaling issues

**Problem:** The UI looks tiny on a high-resolution display.

**Solution:**
Increase the font size under Settings. Kivy may not auto-scale on all systems.

## Tag Issues

### Tags not saving (MOBI/AZW)

**Problem:** Tags disappear after saving.

**Solution:**
MOBI/AZW files use OPF sidecar files. Check if an OPF file was created next to the book. Ensure write permissions in the folder.

### Tags not saving (PDF)

**Problem:** PDF tags don't persist.

**Solutions:**
1. Some PDFs can't be modified (encryption, structure)
2. Run `check_pdf_tags.py` to identify problematic PDFs
3. Problematic PDFs use OPF sidecar files automatically

### Tags not reading from Calibre

**Problem:** Calibre tags are not visible in Libiry.

**Solution:**
Calibre stores tags differently. For PDFs, Calibre uses the subject field while Libiry uses Keywords. Use OPF sidecar files for consistent storage.

## Search issues

### Search isn't finding books

**Problem:** Books exist but search doesn't find them.

**Solutions:**
1. Search is case-insensitive but exact by default
2. Enable Fuzzy search in Settings for partial matches
3. Search depth is limited to 10 folder levels
4. Check if files have correct extensions

### Fuzzy search too broad

**Problem:** Fuzzy search returns too many results.

**Solution:**
Disable fuzzy search for more precise matching:
```ini
Fuzzy search y/n: N
```

## Performance issues

### High memory usage

**Problem:** Libiry uses too much RAM.

**Solutions:**
1. Close other applications
2. Reduce grid zoom level
3. Divide large folders into subfolders

### Slow scrolling

**Problem:** Grid scrolling is laggy.

**Solutions:**
1. Reduce the number of visible tiles (zoom out less)
2. Make sure that thumbnail cache is working (`~/.libiry/cache/`)
3. Use an SSD for library storage

## File issues

### "Permission denied" when saving

**Problem:** Can't save tags or move files.

**Solutions:**
1. Check folder permissions
2. Close files in other applications
3. Run as administrator (Windows)
4. Check if files are read-only

### Deleted files still showing

**Problem:** Removed files appear in grid.

**Solution:**
Press F5 to refresh the view.

### Moving files fails

**Problem:** Move operation doesn't work.

**Solutions:**
1. Check if the destination folder exists
2. Check the write permissions
3. Make sure that the file isn't open in another program

## Getting help

### Debug mode

Run with console output to see error messages:
```batch
run_debug.bat
```

### Log files

Check for errors in the console output. No separate log files are created.

### Reporting issues

When reporting bugs, include:
1. Operating system and version
2. Python version (`python --version`)
3. Error message from debug mode
4. Steps to reproduce
5. Example files

Report issues at: [GitHub Issues](https://github.com/sappelen/Libiry/issues) or [Reddit](https://www.reddit.com/r/libiry/). Please take into account that I am just one person, doing this free of charge.
