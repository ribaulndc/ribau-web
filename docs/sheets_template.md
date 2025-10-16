# 📊 Google Sheets Template

Template and examples for your RiBau product catalog sheet.

---

## 🎯 Sheet Setup

### Sheet Name
**Must be exactly:** `Products` (case-sensitive!)

### Column Headers (Row 1)

Copy and paste these headers into your first row:

```
id	name	description	category	price	inStock	featured
```

Or create them manually in this exact order:

| Column | Header | Type | Required | Notes |
|--------|--------|------|----------|-------|
| A | id | Text | ✅ Yes | 3-digit ID (001, 002, etc.) |
| B | name | Text | ✅ Yes | Product name |
| C | description | Text | ✅ Yes | Short description |
| D | category | Text | ✅ Yes | Category name |
| E | price | Number | ✅ Yes | Price in euros (e.g., 15.00) |
| F | inStock | TRUE/FALSE | ✅ Yes | Product availability |
| G | featured | TRUE/FALSE | ✅ Yes | Show star badge |

---

## 📝 Example Products

Here are example products you can use to test:

### Row 2:
```
001 | Ciotola Ceramica Rossa | Ciotola resistente in ceramica rossa, perfetta per cani di taglia media | Ciotole | 15.00 | TRUE | FALSE
```

### Row 3:
```
002 | Guinzaglio Nylon Blu | Guinzaglio resistente in nylon blu, lunghezza 1.5 metri | Guinzagli | 12.00 | TRUE | TRUE
```

### Row 4:
```
003 | Palla Gioco Gomma | Palla in gomma naturale rimbalzante, ideale per il gioco | Giochi | 8.50 | TRUE | FALSE
```

### Row 5:
```
004 | Cuccia Morbida | Cuccia morbida e confortevole, lavabile in lavatrice | Cucce | 35.00 | FALSE | FALSE
```

### Row 6:
```
005 | Collare Regolabile | Collare in nylon regolabile con fibbia di sicurezza | Collari | 10.00 | TRUE | TRUE
```

---

## 🎨 Categories Suggestions

Suggested categories (you can create your own):

- Ciotole (Bowls)
- Guinzagli (Leashes)
- Collari (Collars)
- Giochi (Toys)
- Cucce (Beds)
- Accessori (Accessories)
- Abbigliamento (Clothing)
- Igiene (Grooming)
- Trasportini (Carriers)

**Tip:** Keep category names consistent! "Ciotole" and "ciotole" are different.

---

## 📋 Field Guidelines

### ID Field
- **Format:** 3 digits with leading zeros
- **Examples:** 001, 002, 025, 099, 100
- **Must match image filenames!**
- **Sequential recommended** (but not required)
- **Unique required** (no duplicates!)

### Name Field
- **Length:** Keep under 50 characters
- **Style:** Capitalize properly (e.g., "Ciotola Rossa" not "ciotola rossa")
- **Avoid:** Special characters, emojis
- **Good:** "Guinzaglio Nylon Blu 1.5m"
- **Bad:** "guinzaglio!!!", "Leash 🐕"

### Description Field
- **Length:** 1-3 sentences (100-200 characters ideal)
- **Content:** Describe features, size, material
- **Good:** "Ciotola resistente in ceramica rossa, perfetta per cani di taglia media"
- **Bad:** "Nice bowl" (too short)

### Category Field
- **Consistency:** Use the same spelling/capitalization
- **Check existing:** Before creating new, check if category exists
- **Good:** All products use "Ciotole"
- **Bad:** Mix of "Ciotole", "ciotole", "Bowls"

### Price Field
- **Format:** Number with 2 decimals (15.00, not 15)
- **Currency:** In euros (€)
- **Don't include:** € symbol in the sheet (just the number)
- **Good:** 15.00
- **Bad:** €15, 15, 15,00 (comma instead of period)

### inStock Field
- **Only use:** TRUE or FALSE (all caps)
- **Don't use:** Yes/No, 1/0, true/false, Si/No
- **Good:** TRUE
- **Bad:** true, yes, 1

### featured Field
- **Same as inStock:** Only TRUE or FALSE
- **Purpose:** Featured products get a ⭐ badge
- **Use sparingly:** Maybe 2-3 products as featured
- **Good:** FALSE
- **Bad:** false, no, 0

---

## ✅ Data Validation (Optional but Recommended)

To prevent errors, you can add data validation in Google Sheets:

### For inStock column (F):
1. Select column F (except header)
2. Data → Data validation
3. Criteria: List of items: `TRUE,FALSE`
4. Reject invalid inputs

### For featured column (G):
Same as above - select column G, add validation for `TRUE,FALSE`

### For category column (D):
1. Select column D (except header)
2. Data → Data validation
3. Criteria: List of items: `Ciotole,Guinzagli,Collari,Giochi,Cucce,Accessori`
4. This creates a dropdown with your categories!

---

## 🎯 Best Practices

### Before Adding Products:
1. ✅ Check the last ID in the sheet
2. ✅ Confirm images are uploaded (check with tech person)
3. ✅ Choose category from existing list
4. ✅ Double-check spelling

### After Adding Products:
1. ✅ Verify all required fields are filled
2. ✅ Check TRUE/FALSE are uppercase
3. ✅ Confirm price uses period (15.00) not comma (15,00)
4. ✅ Wait 30 minutes, check website

### Editing Products:
1. ✅ Find the correct row
2. ✅ Change only what needs updating
3. ✅ Don't delete rows (mark inStock as FALSE instead)
4. ✅ Changes appear on website in ~30 minutes

---

## 🔄 Common Operations

### Adding New Product:
```
1. Coordinate with tech person for images & ID
2. Add new row at the bottom
3. Fill all 7 columns
4. Save (auto-saves in Google Sheets)
5. Wait 30 minutes
```

### Marking as Sold:
```
1. Find product row
2. Change column F (inStock) from TRUE to FALSE
3. Done! Website will show "Non Disponibile"
```

### Changing Price:
```
1. Find product row
2. Edit column E (price)
3. Use format: 15.00 (with period, 2 decimals)
4. Save
```

### Making Featured:
```
1. Find product row
2. Change column G (featured) from FALSE to TRUE
3. Product will show ⭐ badge on website
```

### Removing Product:
```
❌ Don't delete the row! (breaks sync)
✅ Instead: Set inStock to FALSE
```

---

## 📊 Sample Sheet View

Here's how your sheet should look:

```
┌─────┬──────────────────────┬────────────────────┬────────────┬────────┬─────────┬──────────┐
│ id  │ name                 │ description        │ category   │ price  │ inStock │ featured │
├─────┼──────────────────────┼────────────────────┼────────────┼────────┼─────────┼──────────┤
│ 001 │ Ciotola Ceramica     │ Ciotola resistente │ Ciotole    │ 15.00  │ TRUE    │ FALSE    │
│ 002 │ Guinzaglio Nylon     │ Guinzaglio 1.5m    │ Guinzagli  │ 12.00  │ TRUE    │ TRUE     │
│ 003 │ Palla Gioco          │ Palla in gomma     │ Giochi     │  8.50  │ TRUE    │ FALSE    │
│ 004 │ Cuccia Morbida       │ Cuccia lavabile    │ Cucce      │ 35.00  │ FALSE   │ FALSE    │
└─────┴──────────────────────┴────────────────────┴────────────┴────────┴─────────┴──────────┘
```

---

## 🚨 Common Mistakes to Avoid

### ❌ Wrong:
```
id: 1 (needs leading zeros → 001)
id: A1 (letters not allowed)
name: [empty] (required field)
price: €15.00 (remove € symbol)
price: 15,00 (use period not comma)
inStock: yes (must be TRUE or FALSE)
inStock: true (must be uppercase TRUE)
category: Ciotole  (extra spaces)
```

### ✅ Correct:
```
id: 001
name: Ciotola Rossa
price: 15.00
inStock: TRUE
category: Ciotole
```

---

## 📱 Mobile Editing

You can edit the sheet from your phone using the Google Sheets app:

1. Open Google Sheets app
2. Find "RiBau Products"
3. Tap on a cell to edit
4. Changes auto-save
5. Website updates in ~30 minutes

**Tip:** Use data validation (dropdowns) to make mobile editing easier!

---

## 🔍 Troubleshooting

### Product not showing on website after 30+ minutes

**Check:**
1. ✅ Is the row filled completely?
2. ✅ Is inStock set to TRUE?
3. ✅ Is the ID unique (not used by another product)?
4. ✅ Are there any special characters or spaces in the ID?
5. ✅ Wait a bit longer (can take up to 35 minutes)

### Product shows wrong price

**Check:**
1. ✅ Price column uses period not comma (15.00 not 15,00)
2. ✅ No currency symbols (15.00 not €15.00)
3. ✅ Two decimal places (15.00 not 15)

### Category not showing correctly

**Check:**
1. ✅ Spelling matches exactly with other products
2. ✅ No extra spaces before/after
3. ✅ Capitalization matches (Ciotole not ciotole)

### Image not showing

**This is not a sheet issue!** Images are managed separately:
1. Contact tech person
2. Confirm product ID matches image filename
3. Check if images were uploaded to GitHub

---

## 📈 Bulk Operations

### Adding Multiple Products at Once:

1. **Coordinate IDs first:**
   - Tell tech person: "I'm adding products 015-020"
   - Wait for image confirmation
   
2. **Fill all rows:**
   - Add all 6 products in the sheet
   - Double-check all data
   
3. **Review before saving:**
   - Check IDs are sequential
   - All required fields filled
   - Categories consistent

4. **One save for all:**
   - Google Sheets auto-saves
   - All products sync together in next update

### Updating Multiple Prices:

1. Select all price cells you want to change
2. Edit them one by one or use formulas
3. Ensure format stays as numbers with 2 decimals

---

## 💾 Backup & History

### Google Sheets Auto-Saves:
- Every change is automatically saved
- No need to click "Save"
- Can see who made changes (File → Version history)

### Undo Changes:
- Press Ctrl+Z (or Cmd+Z on Mac)
- Or: File → Version history → See version history
- Restore previous versions if needed

### Who Changed What:
- File → Version history
- See all changes with timestamps
- Can restore old versions if mistake was made

---

## 🎓 Training Volunteers

### Simple 5-Minute Training:

1. **Show the sheet:**
   - "This is where all products live"
   - "Each row is one product"

2. **Explain columns:**
   - "ID comes from tech person"
   - "Name and description: make it clear and appealing"
   - "Category: choose from existing"
   - "Price: always with .00"
   - "inStock: TRUE if available"

3. **Demo adding product:**
   - "Let's add a test product together"
   - Walk through each field
   - Show where it appears on website after 30 min

4. **Demo marking as sold:**
   - "Just change TRUE to FALSE"
   - "That's it!"

5. **Give them this guide:**
   - "Keep this for reference"
   - "Contact me if confused"

---

## 📞 Quick Reference Card

Print this for volunteers:

```
┌─────────────────────────────────────────────────┐
│         RIBAU PRODUCTS - QUICK REFERENCE        │
├─────────────────────────────────────────────────┤
│ Sheet Name: Products                            │
│ Update Frequency: Every 30 minutes              │
├─────────────────────────────────────────────────┤
│ ADDING PRODUCT:                                 │
│ 1. Get ID from tech person                      │
│ 2. Fill ALL 7 columns                           │
│ 3. Use TRUE/FALSE (uppercase)                   │
│ 4. Price format: 15.00 (with period)            │
│ 5. Wait 30 min, check website                   │
├─────────────────────────────────────────────────┤
│ MARKING AS SOLD:                                │
│ 1. Find product row                             │
│ 2. Change inStock to FALSE                      │
│ 3. Done!                                        │
├─────────────────────────────────────────────────┤
│ NEED HELP?                                      │
│ Contact: [YOUR NAME/EMAIL]                      │
└─────────────────────────────────────────────────┘
```

---

## 🎉 You're Ready!

Your Google Sheet is now the source of truth for all products. Keep it organized and updated, and the website will automatically reflect all changes!

**Remember:**
- ✅ Always use correct format (TRUE not true, 15.00 not 15)
- ✅ Coordinate with tech person for new products
- ✅ Be consistent with categories and naming
- ✅ Changes take ~30 minutes to appear
- ✅ Never delete rows, mark as FALSE instead

Happy cataloging! 🐾