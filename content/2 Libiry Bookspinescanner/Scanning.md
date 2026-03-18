
Here's how to get the best results when scanning your bookshelves.
## Taking good photos

### Lighting

**Good lighting is the most important factor for accurate OCR.**

| Condition | Quality | Tip |
|-----------|---------|-----|
| Natural daylight | Excellent | Best results |
| Bright room light | Good | Avoid shadows |
| Dim lighting | Poor | Use flash or add light |
| Direct sunlight | Variable | Watch for glare |

### Angle

- **Straight-on** works best
- Slight angle (up to 15°) is acceptable
- Avoid steep angles that distort text

### Distance

- Close enough that spine text is readable
- Far enough to capture 5-15 books per photo
- Typical distance: 30-60 cm (1-2 feet)

### Focus

- Ensure text is sharp, not blurry
- Tap to focus on your phone's camera
- Hold steady while capturing

## Scanning modes

### Spine mode (default)

Best for: Bookshelves with visible spines

1. Take photo of bookshelf
2. App detects individual spine regions
3. OCR extracts text from each spine
4. Text is searched against book databases

**Tips:**
- Works best with clearly printed spines
- Handles both horizontal and vertical text
- Multiple books per photo

### Barcode mode

Best for: Books with visible ISBN barcodes

1. Enable "Barcode Mode" in settings
2. Point camera at book barcode
3. ISBN is detected automatically
4. Direct lookup in book databases

**Tips:**
- Most accurate method
- Works one book at a time
- Barcode must be visible and clear

## Troubleshooting scans

### "No books detected"

**Causes:**
- Photo too dark
- Spines too small in image
- Poor contrast

**Solutions:**
- Add more light
- Get closer to bookshelf
- Ensure spines face camera

### "Poor OCR results"

**Causes:**
- Blurry photo
- Small or decorative fonts
- Faded or damaged spines

**Solutions:**
- Hold camera steady
- Use Google Cloud Vision (more accurate)
- Manually correct results

### "Wrong book matches"

**Causes:**
- Common words on spine
- Generic titles
- Multiple editions

**Solutions:**
- Use barcode mode for accuracy
- Edit and re-search
- Verify against your actual books

### "Barcode not detected"

**Causes:**
- Barcode damaged or dirty
- Glare on barcode
- Camera too far

**Solutions:**
- Clean the barcode
- Reduce glare
- Move closer

## Optimal shelf setup

For best results:

1. **Arrange books vertically** with spines facing out
2. **Remove dust jackets** if they cover spine text
3. **Ensure even lighting** across the shelf
4. **Group by size** if possible (easier detection)

## Batch scanning

For large libraries:

1. Scan one shelf at a time
2. Review each batch before exporting
3. Merge exports in Libiry

This approach:
- Keeps photo quality high
- Makes review manageable
- Reduces memory usage

## Mobile tips

### Android

- Use Chrome for best PWA support
- Install app for faster access
- Grant camera permission permanently

### iOS

- Use Safari (required for PWA)
- Add to Home Screen for app-like experience
- Photos may need good lighting (no flash)

# Phone camera vs. desktop upload -- why results may differ

When you scan a bookshelf with your phone camera, the results may be different from uploading the same shelf as a photo on desktop. This is normal and has several causes:

- **Resolution:** Phone cameras compress the photo before sending it to the app. The uploaded photo on desktop is usually the original, uncompressed file with more detail.
- **Focus and sharpness:** A phone camera may not focus perfectly on every spine, especially at the edges of the frame. A carefully taken photo that you upload later may be sharper.
- **Lighting:** Phone photos taken in indoor lighting often have more noise and less contrast than well-lit photos.
- **Camera angle:** A slight angle or tilt causes perspective distortion, making some spines harder to read.

**Tips for better phone results:**

- Hold the phone steady and straight in front of the bookshelf
- Make sure there is good, even lighting (avoid shadows across the spines)
- Take the photo from a distance where all spines are readable to the human eye
- If results are poor, try taking multiple photos of smaller sections of the shelf
- Use Google Cloud Vision instead of Tesseract for significantly better results on phone photos