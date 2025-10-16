# 📸 Image Naming Guide - Quick Reference

Simple guide for managing product images.

---

## ✅ Correct Naming Examples

```
001_1.jpg  ← Product ID 001, Image 1 (REQUIRED)
001_2.jpg  ← Product ID 001, Image 2 (optional)
001_3.jpg  ← Product ID 001, Image 3 (optional)

025_1.png  ← Product ID 025, Image 1
025_2.png  ← Product ID 025, Image 2

100_1.jpeg ← Product ID 100, Image 1
```

---

## ❌ Wrong Naming Examples

```
❌ bowl_1.jpg          (use product ID, not name)
❌ 001_main.jpg        (use numbers 1,2,3 not words)
❌ 1_1.jpg             (use leading zeros: 001)
❌ 001-1.jpg           (use underscore _, not dash -)
❌ 001_1.JPG           (use lowercase .jpg)
❌ 001 _1.jpg          (no spaces!)
```

---

## 📝 Naming Rules

1. **Format:** `{ID}_{NUMBER}.{extension}`
2. **ID:** 3 digits with leading zeros (001, 002, ... 099, 100)
3. **Number:** 1, 2, or 3 (max 3 images per product)
4. **Extension:** .jpg, .jpeg, or .png (lowercase)
5. **No spaces, no dashes, no special characters**

---

## 🖼️ Image Specifications

| Property | Recommendation |
|----------|---------------|
| Size | 800x800px or 1000x1000px |
| Aspect Ratio | Square (1:1) preferred |
| File Size | < 200KB per image |
| Format | JPG (preferred) or PNG |
| Quality | Good enough to see details |

---

## 🔄 Workflow: Adding New Product Images

### Step 1: Get Images from Volunteer
- Volunteer sends 1-3 photos via email/WhatsApp
- They tell you the product name

### Step 2: Check Next ID
- Open Google Sheet
- Look at last product ID (e.g., 025)
- Next ID is 026

### Step 3: Rename Images
```bash
# Original filenames from volunteer:
red_bowl_front.jpg
red_bowl_side.jpg

# Rename to:
026_1.jpg
026_2.jpg
```

### Step 4: Optimize (Optional but Recommended)
- Go to https://tinypng.com/
- Drag your images
- Download compressed versions
- Saves bandwidth and loads faster!

### Step 5: Add to Repository
```bash
# Place in the products folder
cp 026_*.jpg /path/to/repo/public/images/products/

# Or drag & drop if using GitHub Desktop/VS Code
```

### Step 6: Commit & Push
```bash
git add public/images/products/026_*.jpg
git commit -m "Add images for product 026 - Red Bowl"
git push
```

### Step 7: Notify Volunteer
Message: "✓ Images uploaded! Product ID is 026. You can add it to the sheet now."

---

## 🗂️ Folder Structure

```
public/
└── images/
    ├── lobo_fallback.jpeg  ← Default image when product image missing
    └── products/           ← All product images go here
        ├── 001_1.jpg
        ├── 001_2.jpg
        ├── 001_3.jpg
        ├── 002_1.jpg
        ├── 002_2.png
        ├── 003_1.jpg
        └── ...
```

---

## 🎯 Tips for Better Images

### Good Photos:
- ✅ Clear, well-lit product photos
- ✅ Plain background (white or neutral)
- ✅ Product fills most of the frame
- ✅ In focus and sharp
- ✅ Multiple angles (front, side, detail)

### Avoid:
- ❌ Blurry photos
- ❌ Poor lighting (too dark)
- ❌ Busy backgrounds
- ❌ Product too small in frame
- ❌ Watermarks or text overlays

---

## 🔍 Checking Images on Website

### Image Load Order:
1. Website tries `{ID}_1.jpg` first
2. If not found, tries `{ID}_1.jpeg`
3. If not found, tries `{ID}_1.png`
4. If none found, shows fallback image (Lobo)

### Carousel Navigation:
- If product has 2+ images, arrows and dots appear
- Users can click arrows or dots to see all images
- First image (`_1`) is always the main image

---

## 📊 Quick Checklist

Before committing images:

- [ ] Images named correctly (`001_1.jpg` format)
- [ ] IDs match what's in Google Sheet
- [ ] At least `_1` image exists for each product
- [ ] Images are optimized (< 200KB each)
- [ ] Files are in `public/images/products/` folder
- [ ] Committed and pushed to GitHub
- [ ] Volunteer notified of product ID

---

## 🆘 Common Issues

### Issue: Image doesn't show on website

**Solutions:**
1. Check filename exactly matches format
2. Clear browser cache (Ctrl+Shift+R / Cmd+Shift+R)
3. Check GitHub - is file actually in products folder?
4. Open browser console (F12) - look for 404 error
5. Verify the product ID matches between sheet and filename

### Issue: Wrong image shows

**Cause:** Multiple files with similar names
**Solution:** Check for duplicates, delete incorrect ones

### Issue: Image is huge/slow to load

**Solution:** Compress the image using TinyPNG.com

---

## 💡 Pro Tips

1. **Batch Processing:**
   - If adding 10 products at once, rename all images first
   - Use a text file to track which images go to which ID
   - Commit all at once with one message

2. **Backup Original Images:**
   - Keep a backup folder of original high-res images
   - GitHub has size limits, so don't commit huge files

3. **Consistent Style:**
   - Try to keep similar lighting and background
   - Makes the catalog look more professional

4. **Test Locally:**
   - Before pushing, run website locally
   - Check images load correctly
   - Saves time vs. pushing and waiting for deploy

---

## 📝 Example: Complete Workflow

```
Volunteer: "Hi! Here are photos of a blue leash"
[Sends 2 photos]

You:
1. Download photos: leash1.jpg, leash2.jpg
2. Check sheet: Last product is 037
3. Rename: 038_1.jpg, 038_2.jpg
4. Optimize: Upload to TinyPNG, download compressed
5. Move to: public/images/products/
6. Commit: git add public/images/products/038_*.jpg
7. Commit: git commit -m "Add product 038 - Blue Leash images"
8. Push: git push
9. Reply: "✓ Images ready! Use ID 038 in the sheet"

Volunteer:
1. Opens Google Sheet
2. Adds row: 038 | Guinzaglio Blu | ... | 12.00 | TRUE | FALSE
3. Waits 30 minutes
4. Checks website - leash appears with carousel!
```

---

That's it! Keep this guide handy for quick reference. 🐾