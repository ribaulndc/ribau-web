# 🐾 RiBau Product Catalog - Complete Implementation

Automated product catalog system with Google Sheets sync for Canile di Varese.

---

## 📚 What You've Received

I've created a complete system with the following files:

### 1. **GitHub Action Workflow** (`sync-sheets.yml`)
   - Automatically syncs Google Sheets to CSV every 30 minutes
   - Can be manually triggered from GitHub Actions tab
   - Validates data and checks for missing images

### 2. **Sync Script** (`sync-sheets.js`)
   - Fetches data from Google Sheets API
   - Converts to CSV format
   - Validates image files exist
   - Commits changes to repository

### 3. **Vue Components** (Refactored for maintainability)
   - **ProductCatalog.vue**: Main catalog with filters and loading
   - **ProductCard.vue**: Individual product card with 3-image carousel
   - **ContactForm.vue**: Modal form for product inquiries

### 4. **Documentation**
   - **SETUP_GUIDE.md**: Complete setup instructions
   - **IMAGE_NAMING_GUIDE.md**: Image management reference
   - **GOOGLE_SHEETS_TEMPLATE.md**: Sheet structure and examples

### 5. **Configuration**
   - **package.json**: Dependencies and scripts

---

## 🎯 Key Features

### For You (Admin):
- ✅ Manage images via Git (familiar workflow)
- ✅ Control image quality and optimization
- ✅ Clear naming convention (001_1.jpg)
- ✅ Automatic validation of missing images
- ✅ Version control for everything

### For Volunteers:
- ✅ Simple Google Sheets interface (they already know!)
- ✅ No technical knowledge required
- ✅ Add/edit products without coding
- ✅ Changes appear automatically (30 min)
- ✅ Mobile-friendly editing

### For Visitors:
- ✅ Beautiful product cards with image carousels
- ✅ Up to 3 images per product (swipeable)
- ✅ Category filtering
- ✅ Contact form for inquiries
- ✅ Fast loading times (optimized images)

---

## 📂 File Structure

```
your-repo/
├── .github/
│   └── workflows/
│       └── sync-sheets.yml          ← GitHub Action (runs every 30 min)
│
├── scripts/
│   └── sync-sheets.js               ← Node.js sync script
│
├── public/
│   ├── data/
│   │   └── products.csv             ← Auto-generated from Google Sheets
│   │
│   └── images/
│       ├── lobo_fallback.jpeg       ← Default fallback image
│       └── products/                ← Product images (you manage)
│           ├── 001_1.jpg
│           ├── 001_2.jpg
│           ├── 001_3.jpg
│           ├── 002_1.jpg
│           └── ...
│
├── src/
│   └── components/
│       ├── ProductCatalog.vue       ← Main catalog component
│       ├── ProductCard.vue          ← Product card with carousel
│       └── ContactForm.vue          ← Contact form modal
│
├── docs/
│   ├── SETUP_GUIDE.md               ← Complete setup instructions
│   ├── IMAGE_NAMING_GUIDE.md        ← Image management guide
│   └── GOOGLE_SHEETS_TEMPLATE.md    ← Sheet template & examples
│
├── package.json                      ← Dependencies
└── README.md                         ← This file
```

---

## 🚀 Quick Start

### Step 1: Set Up Google Sheets (15 minutes)
1. Create Google Sheet named "RiBau Products"
2. Add tab named "Products"
3. Add headers: `id | name | description | category | price | inStock | featured`
4. Add some test products

**See:** `GOOGLE_SHEETS_TEMPLATE.md` for details

### Step 2: Create Google Service Account (10 minutes)
1. Go to Google Cloud Console
2. Create project and enable Sheets API
3. Create service account
4. Download JSON credentials
5. Share sheet with service account email

**See:** `SETUP_GUIDE.md` Section 2

### Step 3: Configure GitHub (5 minutes)
1. Add secrets to GitHub repo:
   - `GOOGLE_SHEETS_ID`: Your sheet ID from URL
   - `GOOGLE_SERVICE_ACCOUNT`: Entire JSON file contents
2. Copy workflow file to `.github/workflows/sync-sheets.yml`
3. Copy sync script to `scripts/sync-sheets.js`

**See:** `SETUP_GUIDE.md` Sections 3-4

### Step 4: Add Files to Repository (5 minutes)
1. Create folder structure
2. Add Vue components
3. Update your main App.vue to use ProductCatalog
4. Install dependencies: `npm install`

### Step 5: Test Everything (10 minutes)
1. Manually trigger GitHub Action
2. Check if CSV is generated
3. Add test product to sheet
4. Wait 30 minutes and verify on website

**See:** `SETUP_GUIDE.md` Section 6

---

## 🖼️ Image Management Workflow

### When Volunteer Wants to Add Product:

```
VOLUNTEER                          YOU                          SYSTEM
    |                              |                              |
    |-- "Here are images" -------->|                              |
    |                              |                              |
    |                              |-- Rename: 026_1.jpg          |
    |                              |-- Optimize images            |
    |                              |-- Git commit & push -------->|
    |                              |                              |
    |<-- "Use ID 026" -------------|                              |
    |                              |                              |
    |-- Add to Google Sheet        |                              |
    |                              |                              |
    |                              |                       [30 min wait]
    |                              |                              |
    |                              |                    Sync runs ⚙️
    |                              |                    Updates CSV
    |                              |                    Deploys site
    |                              |                              |
    |<----- Product visible on website! -------------------------|
```

### Image Naming:
- Format: `{ID}_{NUMBER}.{ext}`
- Example: `001_1.jpg`, `001_2.jpg`, `001_3.jpg`
- Max 3 images per product
- Supported: `.jpg`, `.jpeg`, `.png`

**See:** `IMAGE_NAMING_GUIDE.md` for complete details

---

## 🎨 Component Architecture

### ProductCatalog.vue (Parent)
- Fetches and parses CSV
- Manages category filtering
- Handles modal state
- Renders grid of ProductCard components

### ProductCard.vue (Child)
- Displays single product
- 3-image carousel with arrows and dots
- Handles image errors gracefully
- Emits contact event to parent

### ContactForm.vue (Modal)
- Netlify form integration
- Pre-fills product info
- Validates input
- Shows success/error messages

**Benefits of separation:**
- Easier to maintain and debug
- Reusable components
- Clear responsibility for each component
- Simpler testing

---

## ⚙️ How Auto-Sync Works

1. **GitHub Action triggers** (every 30 minutes or manually)
2. **Script authenticates** with Google Sheets API using service account
3. **Fetches all data** from "Products" tab
4. **Converts to CSV** with proper escaping
5. **Validates** image files exist in repo
6. **Commits CSV** if data changed (with [skip ci] to avoid loops)
7. **Netlify detects** commit and auto-deploys
8. **Website loads** new CSV data

**Time:** Usually completes in 30-60 seconds

---

## 🔧 Maintenance

### Regular Tasks (You):
- Add/optimize images when volunteers request (~5 min/product)
- Monitor GitHub Actions for errors (check weekly)
- Backup Google Sheet periodically (monthly)

### Volunteer Tasks:
- Add/edit products in Google Sheet
- Coordinate with you for new product images
- Mark products as sold (inStock = FALSE)

### Automated:
- Sync runs every 30 minutes automatically
- Website deploys automatically on changes
- No manual intervention needed!

---

## 💰 Costs

- **Google Cloud**: Free (within API limits)
- **GitHub Actions**: Free (2000 minutes/month, you'll use ~50)
- **GitHub Storage**: Free (images total < 100MB)
- **Netlify Hosting**: Free tier (usually sufficient)
- **Total**: $0/month for your scale!

---

## 📊 Scalability

Current setup handles:
- ✅ 50 products easily
- ✅ 150 images (3 per product)
- ✅ ~20MB total image size
- ✅ Low traffic (< 1000 visits/month)

When to consider upgrading:
- 🔄 > 200 products (consider Airtable/CMS)
- 🔄 > 10 volunteers actively editing
- 🔄 High traffic (> 10K visits/month)
- 🔄 Need real-time updates (not 30 min delay)

**For now:** Perfect fit for your needs!

---

## 🆘 Support & Troubleshooting

### Common Issues:

**Products not syncing:**
- Check GitHub Actions tab for errors
- Verify secrets are set correctly
- Ensure sheet is shared with service account

**Images not loading:**
- Verify filename matches format (001_1.jpg)
- Check file is in public/images/products/
- Clear browser cache

**Sheet changes not appearing:**
- Wait full 30 minutes
- Check GitHub Actions ran successfully
- Verify data format (TRUE not true, 15.00 not 15)

**See:** `SETUP_GUIDE.md` Section 8 (Troubleshooting)

---

## 🎓 Training Materials

### For Volunteers:
- Give them: `GOOGLE_SHEETS_TEMPLATE.md`
- Quick reference card (included in template)
- 5-minute walkthrough of adding a product

### For You:
- `IMAGE_NAMING_GUIDE.md` - keep this handy
- Test the workflow a few times
- Create a backup plan (manual CSV edit if needed)

---

## 🔐 Security Notes

- Service account has **read-only** access to sheet
- Credentials stored as **GitHub secrets** (encrypted)
- No sensitive data exposed in code
- Netlify forms handle contact inquiries securely

---

## 🚀 Next Steps

1. **Complete setup** following SETUP_GUIDE.md
2. **Add 5-10 test products** to validate everything works
3. **Train one volunteer** and have them add a product
4. **Monitor for a week** to ensure stability
5. **Onboard remaining volunteers**
6. **Launch!** 🎉

---

## 📝 Future Enhancements (Optional)

Ideas for later:
- Add search functionality
- Product sorting (by price, name, etc.)
- Pagination for large catalogs
- Admin dashboard for analytics
- Email notifications on new inquiries
- Multi-language support

**For now:** Keep it simple and working!

---

## 🙏 Credits

Built with:
- Vue.js 3
- Google Sheets API
- GitHub Actions
- Netlify Forms
- Love for dogs 🐕

---

## 📞 Questions?

If you get stuck:
1. Check the SETUP_GUIDE.md thoroughly
2. Look at GitHub Actions logs for errors
3. Verify all steps in the Quick Start section
4. Double-check the Google Sheets template

Good luck with RiBau! 🐾