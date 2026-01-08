# 🐾 RiBau Product Catalog - Setup Guide

Complete setup instructions for the Google Sheets + GitHub sync system.

---

## 📋 Table of Contents

1. [Google Sheets Setup](#1-google-sheets-setup)
2. [Google Service Account Setup](#2-google-service-account-setup)
3. [GitHub Repository Setup](#3-github-repository-setup)
4. [GitHub Secrets Configuration](#4-github-secrets-configuration)
5. [Image Management Guide](#5-image-management-guide)
6. [Testing the Setup](#6-testing-the-setup)
7. [Volunteer Guide](#7-volunteer-guide)

---

## 1. Google Sheets Setup

### Create the Products Sheet

1. **Create a new Google Sheet** named "RiBau Products"
2. **Create a sheet tab** named "Products" (case-sensitive!)
3. **Add the following headers** in row 1:

```
| id | name | description | category | price | inStock | featured |
```

### Header Explanations:

- **id**: Unique product ID (e.g., 001, 002, 003) - MUST match image filenames
- **name**: Product name (e.g., "Ciotola Rossa")
- **description**: Short description (e.g., "Ciotola in ceramica resistente")
- **category**: Category name (e.g., "Ciotole", "Guinzagli", "Giochi")
- **price**: Price in euros (e.g., 15.00)
- **inStock**: TRUE or FALSE
- **featured**: TRUE or FALSE (featured products get a star badge)

### Example Data:

```
001 | Ciotola Rossa | Ciotola in ceramica resistente | Ciotole | 15.00 | TRUE | FALSE
002 | Guinzaglio Blu | Guinzaglio in nylon 1.5m | Guinzagli | 12.00 | TRUE | TRUE
003 | Palla Gioco | Palla in gomma rimbalzante | Giochi | 8.50 | FALSE | FALSE
```

---

## 2. Google Service Account Setup

This allows GitHub Actions to read your sheet automatically.

### Step 1: Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Click **"Create Project"**
3. Name it "RiBau Sync" and create

### Step 2: Enable Google Sheets API

1. In your project, go to **"APIs & Services" > "Library"**
2. Search for **"Google Sheets API"**
3. Click **"Enable"**

### Step 3: Create Service Account

1. Go to **"APIs & Services" > "Credentials"**
2. Click **"Create Credentials" > "Service Account"**
3. Name: "ribau-sheets-reader"
4. Click **"Create and Continue"**
5. Skip optional steps, click **"Done"**

### Step 4: Generate JSON Key

1. Click on the service account you just created
2. Go to **"Keys"** tab
3. Click **"Add Key" > "Create New Key"**
4. Choose **JSON** format
5. **Download the JSON file** - you'll need this later!

### Step 5: Share Sheet with Service Account

1. Open your Google Sheet
2. Click **"Share"** button
3. Copy the service account email from the JSON file (looks like: `ribau-sheets-reader@your-project.iam.gserviceaccount.com`)
4. Paste it in the share dialog
5. Give **"Viewer"** permissions
6. Uncheck "Notify people"
7. Click **"Share"**

---

## 3. GitHub Repository Setup

### Project Structure

Create the following folder structure in your repo:

```
your-repo/
├── .github/
│   └── workflows/
│       └── sync-sheets.yml        (GitHub Action workflow)
├── scripts/
│   └── sync-sheets.js             (Sync script)
├── public/
│   ├── data/
│   │   └── products.csv           (Generated automatically)
│   └── images/
│       ├── lobo_fallback.jpeg     (Fallback image)
│       └── products/              (Product images folder)
│           ├── 001_1.jpg
│           ├── 001_2.jpg
│           ├── 001_3.jpg
│           ├── 002_1.jpg
│           └── ...
├── src/
│   └── components/
│       ├── ProductCatalog.vue
│       ├── ProductCard.vue
│       └── ContactForm.vue
└── package.json
```

### Install Dependencies

Add to your `package.json`:

```json
{
  "dependencies": {
    "vue": "^3.3.0"
  },
  "devDependencies": {
    "googleapis": "^126.0.0"
  }
}
```

---

## 4. GitHub Secrets Configuration

### Step 1: Get Your Sheet ID

From your Google Sheet URL:
```
https://docs.google.com/spreadsheets/d/1ABC123XYZ456/edit
                                      ^^^^^^^^^^^^^^
                                      This is your Sheet ID
```

### Step 2: Add Secrets to GitHub

1. Go to your GitHub repository
2. Click **"Settings"** > **"Secrets and variables"** > **"Actions"**
3. Click **"New repository secret"**

Add these two secrets:

#### Secret 1: `GOOGLE_SHEETS_ID`
- Name: `GOOGLE_SHEETS_ID`
- Value: Your sheet ID (from Step 1)

#### Secret 2: `GOOGLE_SERVICE_ACCOUNT`
- Name: `GOOGLE_SERVICE_ACCOUNT`
- Value: The **entire contents** of the JSON file you downloaded earlier
- Paste the whole JSON (starts with `{` and ends with `}`)

---

## 5. Image Management Guide

### Image Naming Convention

Images MUST follow this exact naming pattern:

```
{PRODUCT_ID}_{IMAGE_NUMBER}.{extension}
```

**Examples:**
- `001_1.jpg` - First image for product 001
- `001_2.jpg` - Second image for product 001
- `001_3.jpg` - Third image for product 001
- `002_1.png` - First image for product 002

**Supported formats:** `.jpg`, `.jpeg`, `.png`

### Image Requirements

- **Maximum 3 images per product**
- **At least 1 image required** (the `{ID}_1.jpg`)
- **Recommended size:** 800x800px or 1000x1000px
- **Recommended file size:** < 200KB per image
- **Format:** JPG (preferred) or PNG

### How to Add Images (Your Process)

1. **Volunteer sends you images** via email/WhatsApp with product name
2. **Check the next available ID** in Google Sheet (e.g., if last product is 025, next is 026)
3. **Rename images:**
   - `026_1.jpg` (main image)
   - `026_2.jpg` (optional second image)
   - `026_3.jpg` (optional third image)
4. **Optional: Optimize images**
   - Use [TinyPNG.com](https://tinypng.com/) or [Squoosh.app](https://squoosh.app/)
   - Drag & drop images to compress
5. **Add to repository:**
   ```bash
   # Place images in public/images/products/
   git add public/images/products/026_*.jpg
   git commit -m "Add images for product 026"
   git push
   ```
6. **Tell volunteer:** "Images uploaded! You can add product 026 to the sheet now"

### Image Optimization Tips

**Quick method (online):**
- Go to [TinyPNG.com](https://tinypng.com/)
- Drag images
- Download compressed versions
- Usually reduces size by 60-70%

**Batch processing (if you have many):**
- Use ImageOptim (Mac) or FileOptimizer (Windows)
- Drag entire folder
- Saves automatically

---

## 6. Testing the Setup

### Test 1: Manual GitHub Action Run

1. Go to your GitHub repo
2. Click **"Actions"** tab
3. Click **"Sync Google Sheets to CSV"** workflow
4. Click **"Run workflow"** dropdown
5. Click green **"Run workflow"** button
6. Wait ~30 seconds
7. Check if `public/data/products.csv` was created/updated

### Test 2: Add a Test Product

1. In Google Sheet, add a test row:
   ```
   999 | Test Product | This is a test | Test | 1.00 | TRUE | FALSE
   ```
2. Wait 30 minutes (or manually trigger the action)
3. Check your website - should see the new product

### Test 3: Image Loading

1. Add a test image: `public/images/products/999_1.jpg`
2. Commit and push
3. Visit your website
4. The test product should show your image

---

## 7. Volunteer Guide

Simple instructions for non-technical team members.

### For Volunteers: How to Add a Product

1. **Get the next available ID:**
   - Look at the last row in the sheet
   - Add 1 to that ID
   - Example: If last is 025, use 026

2. **Send images to Matteo Bordignon:**
   - WhatsApp/Email: "Hi! Here are images for the new [product name]"
   - Attach 1-3 photos
   - Wait for confirmation

3. **Add product to Google Sheet:**
   - Fill in all columns:
     - **id**: The ID Matteo confirmed (e.g., 026)
     - **name**: Product name
     - **description**: Short description (1-2 sentences)
     - **category**: Choose existing or create new
     - **price**: Price in euros (e.g., 15.00)
     - **inStock**: TRUE (if available) or FALSE
     - **featured**: TRUE (to highlight) or FALSE

4. **Wait 30 minutes:**
   - The website updates automatically every 30 minutes
   - Check the website to see your product!

### For Volunteers: How to Edit a Product

1. **Find the product row** in Google Sheet
2. **Edit the field** you want to change
3. **Save** (Google Sheets auto-saves)
4. **Wait 30 minutes** for website to update

### For Volunteers: Mark Product as Sold

1. Find the product row
2. Change **inStock** from TRUE to FALSE
3. Website will show "Non Disponibile" in 30 minutes

---

## 🚨 Troubleshooting

### Products not showing on website

**Check:**
1. Is the Google Sheet shared with the service account?
2. Are GitHub secrets set correctly?
3. Did the GitHub Action run successfully? (Check Actions tab)
4. Is the Sheet tab named exactly "Products"?

### Images not loading

**Check:**
1. Are images named correctly? (`001_1.jpg`)
2. Are images in `public/images/products/` folder?
3. Did you commit and push images?
4. Check browser console for 404 errors

### GitHub Action failing

**Check:**
1. Secrets are set (GOOGLE_SHEETS_ID and GOOGLE_SERVICE_ACCOUNT)
2. Service account JSON is complete (starts with `{`, ends with `}`)
3. Google Sheets API is enabled in Google Cloud Console

---

## 📞 Need Help?

If something isn't working:
1. Check the GitHub Actions logs (Actions tab > latest run > click on it)
2. Look for error messages
3. Check the troubleshooting section above

---

## 🎉 You're All Set!

Once everything is configured:
- Volunteers add products to Google Sheets
- You add images to GitHub
- Website updates automatically every 30 minutes
- No manual CSV editing needed!